---
layout: post
title: "[Design] Big Data - Remove Duplicate Numbers"
comments: true
category: Design

---

### Question 

[link](http://blog.csdn.net/v_JULY_v/article/details/6279498)

> 2.5亿个整数中找出不重复的整数的个数，内存空间不足以容纳这2.5亿个整数。

### Analysis

Categorized under __双层桶划分__ or __BitMap__. 

整数个数为2^32,也就是，我们可以将这2^32个数，划分为2^8个区域(比如用单个文件代表一个区域)，然后将数据分离到不同的区域，然后不同的区域在利用bitmap就可以直接解决了。

__But how exactly to use BitMap__? 将bit-map扩展一下，用2bit表示一个数即可，0表示未出现，1表示出现一次，2表示出现2次及以上。
