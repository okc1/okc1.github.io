---
layout: post
title: "[Question] Partition Problem (divide array into halves) "
comments: true
category: Question
tags: [  ]
---

# Question

[link](http://www.geeksforgeeks.org/dynamic-programming-set-18-partition-problem/)

> [partition problem](https://en.wikipedia.org/wiki/Partition_problem) is the task of deciding whether a given multiset S of positive integers can be partitioned into two subsets S1 and S2 such that the sum of the numbers in S1 equals the sum of the numbers in S2.  

> Examples

    arr[] = {1, 5, 11, 5}
    Output: true 
    The array can be partitioned as {1, 5, 5} and {11}

    arr[] = {1, 5, 3}
    Output: false 
    The array cannot be partitioned into equal sum sets.

# Solution

__DP__ (only if sum of the elements is not too big).

> [We can create a 2D array](http://www.geeksforgeeks.org/dynamic-programming-set-18-partition-problem/) of size (sum/2)*(n+1). And we can construct the solution in bottom up manner such that every filled entry has following property:

    part[i][j] = 
        true if a subset of {arr[0], arr[1], ..arr[j-1]} has sum equal to i
        false otherwise

Note that we always cares about __whether there exist a valid subset from beginning to index i__. 

Example DP array for input "3,1,1,2,2,1":

{% img middle /assets/images/partition-problem-dp.jpg %}

# Code
