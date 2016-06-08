---
layout: post
title: "[CC150v4] 20.12 Sub-matrix with Largest Sum "
comments: true
category: CC150v4

---

### Question

> Given an NxN matrix of positive and negative integers, write code to find the sub-matrix with the largest possible sum. 

### Solution

I wrote about this question before: __[Question] Max Sum In A 2D Array (sub-matrix)__, and the solution gave a better time complexity (O(n^3)) than in the book (O(n^4)). 

1. locate a row - O(n)
1. locate another row - O(n)
1. compute sub value of that column - O(n), and then find largest subarray in array - also O(n)
1. The above 3 steps each take O(n) time, total time is O(n^3). 

Please refer to the other post for more detail. 
