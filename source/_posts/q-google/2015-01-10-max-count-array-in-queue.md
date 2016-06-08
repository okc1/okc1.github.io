---
layout: post
title: "[Google] Maximum Count Array in a Queue "
comments: true
category: q-google

---

### Question 

[link1](http://www.mitbbs.com/article_t1/JobHunting/32856675_0_1.html#top)

> 给一个数组a[n]，令s[i]为a[i+1..n-1]中比a[i]大的数的数量。

> 求最大的s[i]。要求O(nlogn)

### Solution

This is very similar question to __[Google] Form a Queue Given Heights__. The idea is to insert elements into BST and count number of larger elements. 

Naitive solution can be reached with a list. 
