---
layout: post
title: "[Fundamental] Suffix Array "
comments: true
categories:
- Fundamental
- z-string-search

---

[ref](http://www.geeksforgeeks.org/suffix-array-set-1-introduction/)

### Suffix Array

A suffix array is a sorted array of all suffixes of a given string. 

__Any suffix tree based algorithm__ can be replaced with an algorithm __that uses a suffix array__ enhanced with additional information and solves the same problem in the same time complexity. 

__Naive algorithm__ for construction of suffix array is to consider all suffixes, sort them using a O(nLogn) sorting algorithm and while sorting, maintain original indexes. Time complexity is _O(n^2 * Logn)__. 

There is an advanced __nLogn Algorithm__ algorithm available to read [here](http://www.geeksforgeeks.org/suffix-array-set-2-a-nlognlogn-algorithm/). Basic idea is to "Sort according to first two characters" and then "according to first four character". 

Example question: __[Facebook] Query Search (HashMap, suffix array)__. 
