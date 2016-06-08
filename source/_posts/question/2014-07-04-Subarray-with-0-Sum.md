---
layout: post
title: "[Question] Subarray with 0 Sum"
comments: true
category: Question
tags: [ unit test needed ]
---

### Question 

[link](http://www.geeksforgeeks.org/find-if-there-is-a-subarray-with-0-sum/)

> Given an array of positive and negative numbers, find if there is a subarray with 0 sum.

> eg. 4, 2, -3, 1, 6 -> return true (2, -3, 1)
>
> eg. 4, 2, 0, 1, 6 -> return true (0)

### Solution

__General case__, idea of 前缀和: 

> iterate through the array and for every element arr[i], calculate sum of elements form 0 to i (this can simply be done as sum += arr[i]). If the current sum has been seen before, then there is a zero sum array. 

O(n) time. 

__Special Case__, if the input is all positive number, then this question can be solved using the idea from __Subarray with Particular Sum__, O(n) time. 
