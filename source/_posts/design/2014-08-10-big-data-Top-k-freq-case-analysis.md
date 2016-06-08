---
layout: post
title: "[Design] Big Data - Top k Frequency (case analysis)"
comments: true
categories:
- Design
- z-top-K

---

### Question 

[link](http://dongxicheng.org/big-data/select-ten-from-billions/)

> 在海量数据中找出出现频率最高的前K个数，或者从海量数据中找出最大的前K个数，这类问题通常称为“top K”问题，

> 1. top K value
> 1. top K frequency

### Analysis

__Standard solution__ is 【分治+trie树/hash+小顶堆/quickselect】, which I covered in another post [Big Data - Top k Frequency]({% post_url /design/2014-07-25-big-data-Top-k-frequency %}). Briefly it is 3 steps: 

1. 先将数据集按照hash方法分解成多个小数据集，
1. 使用trie树或者hash统计每个小数据集中的query词频，
1. 用小顶堆/quickselect求出每个数据集中出频率最高的前K个数

But, there're other senarios where different solutions may apply. Consider: 

1. Single core vs. multiple core

1. Single PC vs. multiple PC

1. Large RAM vs. limited RAM

1. Distributed system

### 1. 单机+单核+足够大内存

设每个查询词平均占8Byte，则10亿个查询词所需的内存大约是10^9*8=8G内存。如果你有这么大的内存，直接在内存中对查询词进行排序，顺序遍历找出10个出现频率最大的10个即可。这种方法简单快速，更加实用。当然，也可以先用HashMap求出每个词出现的频率，然后求出出现频率最大的10个词。

### 2. 单机+单核+受限内存

这种情况下，需要将原数据文件切割成一个一个小文件，如，采用hash(x)%M，将原文件中的数据切割成M小文件，如果小文件仍大于内存大小，继续采用hash的方法对数据文件进行切割，直到每个小文件小于内存大小，这样，每个文件可放到内存中处理。采用3.1节的方法依次处理每个小文件。

### 3. 单机+多核+足够大内存

这时可以直接在内存中实用hash方法将数据划分成n个partition，每个partition交给一个线程处理，线程的处理逻辑是同[1]节类似，最后一个线程将结果归并。

该方法存在一个瓶颈会明显影响效率，即数据倾斜，每个线程的处理速度可能不同，快的线程需要等待慢的线程，最终的处理速度取决于慢的线程。解决方法是，__将数据划分成 (c x n)个partition（c>1），每个线程处理完当前partition后主动取下一个partition继续处理__，直到所有数据处理完毕，最后由一个线程进行归并。

### 4. 多机+受限内存

这种情况下，为了合理利用多台机器的资源，可将数据分发到多台机器上，每台机器采用[3]节中的策略解决本地的数据。可采用__hash + socket__方法进行数据分发。

### 5. Distributed

Top k问题很适合采用__MapReduce框架__解决，用户只需编写一个map函数和两个reduce 函数，然后提交到Hadoop（采用mapchain和reducechain）上即可解决该问题。

A map function. 对于map函数，采用hash算法，将hash值相同的数据交给同一个reduce task. 

2 reduce functions. 对于__第一个reduce函数__，采用HashMap统计出每个词出现的频率，对于__第二个reduce函数__，统计所有reduce task输出数据中的top k即可。

### 6. Other

公司一般不会自己写个程序进行计算，而是提交到自己核心的数据处理平台上计算，该平台的计算效率可能不如直接写程序高，但它具有__良好的扩展性和容错性__，而这才是企业最看重的。
