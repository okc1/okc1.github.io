---
layout: post
title: "[LintCode] Majority Number III"
description: ""
category: LintCode

---

### Question 

[link](http://www.lintcode.com/en/problem/majority-number-iii/)

> Given an array of integers and a number k, the majority number is the number that occurs more than 1/k of the size of the array. Find it.

> Note: There is only one majority number in the array

> Example: For [3,1,2,3,2,3,3,4,4,4] and k = 3, return 3

### Analysis 

Similar to 'Majority Number II', but a little more difficult. 

__Instead of keeping 2 value for checking, now keep k values__. Since values are constantly checked for existance, using a HashMap looks like a great idea. 

__Another idea suggest by [G4G](http://www.geeksforgeeks.org/given-an-array-of-of-size-n-finds-all-the-elements-that-appear-more-than-nk-times/) is a mechanism similar to the famous Tetris Game__. The size of the buffer is k. The buffer is full, we remove all items by counter of 1. When counter reach 0, remove that item. In this way, the elements left in the buffer are the majority numbers. 

This method is also used in counting highly-frequent string keywrods. For example, another post __[Design] Big Data - Real Time Top K__ discusses about it. 

### Code

I did not write code for this question. Shouldn't be difficult. 
