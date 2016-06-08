---
layout: post
title: "[Design] Big Data - Find Existence of a Number"
comments: true
category: Design

---

### Question 

[link](http://blog.csdn.net/v_july_v/article/details/7382693)

> 给40亿个不重复的unsigned int的整数，没排过序的，然后再给一个数，如何快速判断这个数是否在那40亿个数当中？

### Analysis

Categorized under __BitMap__.

There're 4.3 billion unsigned integers in Java. This is a perfect question to use BitMap. 

申请512M的内存，一个bit位代表一个unsigned int值。读入40亿个数，设置相应的bit位，读入要查询的数，查看相应bit位是否为1，为1表示存在，为0表示不存在。
