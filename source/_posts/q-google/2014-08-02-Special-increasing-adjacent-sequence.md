---
layout: post
title: "[Google] Special increasing adjacent sequence"
comments: true
category: q-google

---

### Question 

[link](http://www.careercup.com/question?id=5147801809846272)

> Given a NxN matrix which contains all distinct 1 to n^2 numbers, write code to print sequence of increasing adjacent sequential numbers. 

    ex: 
    1 5 9 
    2 3 8 
    4 6 7 

> should print: 6 7 8 9

### Solution

> Make an array of booleans (or bits) of same size as the input, where arr[i-1] indicates whether i is adjacent to i+1. Then, iterate over the matrix, checking for each cell the four neighbors and populating the relevant entry in the boolean array. 

Last, look for the longest run of "true" values in the boolean array, which can be done with one pass. O(n) time. 

__Note that this algorithm is valid only if input integers are distinct__, which is true here. 

### Code

__not written__
