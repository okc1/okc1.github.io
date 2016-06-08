---
layout: post
title: "[Question] Product Array Puzzle "
comments: true
category: Question

---

### Question 

[link](http://www.geeksforgeeks.org/amazon-interview-set-78-fresher-internship/)

> Given an array of integers , replace each element with the product of the remaining elements.

  Eg : Input - 1 2 3 4     
       Output : 24 12 8 6 

> Do not use division.

### Solution

Store the product of the left side elements for each integer, and also the right side. 

For eg : L[]= {1 , 1 , 2 , 6 }

and R[] = { 24 , 12 , 4 , 1} 

The multiply R[i] and L[i] to get the resultant array.
