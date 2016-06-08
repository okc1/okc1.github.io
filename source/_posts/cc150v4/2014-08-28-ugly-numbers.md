---
layout: post
title: "[CC150v4] 10.7 Ugly Numbers (Hamming numbers) "
comments: true
category: CC150v4

---

### Question

> Design an algorithm to find the kth number such that the only prime factors are 3, 5, and 7. 

### Solution

__This is very difficult question__. All I can say is, just memorize this solution. 

It works like this: 

1. Init 3 queues, with initial value of 3, 5 and 7 respectively. 
1. Fetch the smallest element x at the head of 3 queues. 
1. Add number x to the result list, then: 
    1. if number x comes from queue3, add 3x, 5x and 7x into 3 queues
    1. if number x comes from queue5, add 5x and 7x into queue5 and queue7
    1. if number x comes from queue7, add 7x into queue7
1. Fetch next smallest element and do this recursively.

A [dp solution](http://www.geeksforgeeks.org/ugly-numbers/) is available. It's using the same method actually, but less intuitive. 

### Code

not written
