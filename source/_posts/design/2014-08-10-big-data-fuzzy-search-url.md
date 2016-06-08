---
layout: post
title: "[Design] Big Data - Fuzzy Search url (Bloom Filter) "
comments: true
categories:
- Design
- z-string-search
---

### Question 

[link](http://blog.csdn.net/v_july_v/article/details/7382693)

> 给你A,B两个文件，各存放50亿条URL，每条URL占用64字节，内存限制是4G，让你找出A,B文件共同的URL。如果是三个乃至n个文件呢？

### Bloom Filter

自从Burton Bloom在70年代提出[Bloom Filter](http://blog.csdn.net/v_july_v/article/details/6685894)之后，Bloom Filter就被广泛用于__拼写检查，数据库系统中。。。可以实现数据字典，进行数据的判重，或者集合求交集__

#### 基本原理及要点

An empty Bloom filter is __a bit array of m bits__, all set to 0. There must also be __k different hash functions__ defined, each of which maps or hashes some set element to one of the m array positions with a uniform random distribution. 

很明显这个过程并不保证查找的结果是100%正确的。同时也不支持删除一个已经插入的关键字，因为该关键字对应的位会牵动到其他的关键字。

所以一个简单的改进就是 counting Bloom filter，用一个counter数组代替位数组，就可以支持删除了。 

### Error rate

    m: length of BF array (in bits)
    n: number of input elements
    k: number of hash functions

A Bloom filter [with 1% error](http://en.wikipedia.org/wiki/Bloom_filter#Space_and_time_advantages) and an optimal value of k, in contrast, requires only about 9.6 bits per element (means m = 9.6 x n). 

#### Usage

Bloom Filter可以用来实现数据字典，进行数据的判重，或者集合求交集.

### Solution

Of course we can always use __【分治+trie树/hash+小顶堆】__ standard solution, but for __Fuzzy search, BF is the best__. 

4G = 2^32 大概是40亿 x 8大概是340亿bit，n = 50亿，如果按出错率0.01算需要的大概是480亿个bit。现在可用的是340亿，相差并不多，这样可能会使出错率上升些。
