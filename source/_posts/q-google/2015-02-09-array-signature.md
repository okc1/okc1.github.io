---
layout: post
title: "[Google] Array Signature "
comments: true
category: q-google

---

### Question 

[link](http://www.careercup.com/question?id=14912744)

> You are given an array of n elements [1,2,....n]. For example {3 2 1 4 6 5 7}. 

> Now we create a signature of this array by comparing every consecutive pair of elements. If they increase, write "I" else write "D". 

> For example for the above array, the signature would be "DDIIDI". The signature thus has a length of N-1. 

> Now given a signature, compute the lexicographically __smallest permutation__ of [1,2,....n]. 

### Solution 

A great [answer](http://qr.ae/BPfNw): 

> Take the above case. Signature = DDIIDI.

> Take original permutation as 1 2 3 4 5 6 7.

> Then for first continuous sequence DD reverse the strip 1 2 3 to 3 2 1 hence sequence becomes 3 2 1 4 5 6 7.

> Then for second sequence D reverse strip 5 6 to 6 5 hence sequence becomes 3 2 1 4 6 5 7.

> There is no continuous D left we are done and reached the answer.

### Code

Not written.
