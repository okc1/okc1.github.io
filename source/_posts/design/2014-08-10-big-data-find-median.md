---
layout: post
title: "[Design] Big Data - Find Median Numbers"
comments: true
category: Design

---

### Question 

[link](http://blog.csdn.net/v_july_v/article/details/7382693)

> 5亿个int找它们的中位数.

### Analysis

Categorized under __双层桶划分__.

Idea: 首先我们将int划分为2^16个区域，然后读取数据统计落到各个区域里的数的个数，之后我们根据统计结果就可以判断中位数落到那个区域，同时知道这个区域中的第几大数刚好是中位数。然后第二次扫描我们只统计落在这个区域中的那些数就可以了。

### Details

开一个大小为65536的Int数组，第一遍读取，统计Int32的高16位的情况(就相当于用该数除以65536)。每读取一个数，数组中对应的计数+1。第一遍统计之后，遍历数组，逐个累加统计，看中位数处于哪个区间。

第二遍统计同上面的方法类似，但这次只统计处于区间k的情况，这次计数之后，再统计一下，看中位数所处的区间，最后将高位和低位组合一下就是结果了。

And this can be done more than 2 times, depending on the input size (eg. if input is int64, then do 24/20/20 bits).
