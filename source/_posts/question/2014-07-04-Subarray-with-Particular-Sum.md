---
layout: post
title: "[Question] Subarray with Particular Sum"
comments: true
category: Question
tags: [ unit test needed ]
---

### Question 

[link](http://www.geeksforgeeks.org/find-subarray-with-given-sum/)

> Given an unsorted array of nonnegative integers, find a continous subarray which adds to a given number.

> Eg. input = (1, 4, 20, 3, 10, 5), 33, output (20, 3, 10)

### Solution

Like a sliding window. Note that input numbers are all positive (otherwise it won't work). 

> Initialize a variable 'curr_sum' as first element. 'curr_sum' indicates the sum of current subarray. Start from the second element and add all elements one by one to the curr_sum. 

1. If curr_sum exceeds the sum, then remove first. 
1. If curr_sum becomes equal to sum, solution found.

O(n) time. 
