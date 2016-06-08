---
layout: post
title: "[Design] Multithreading Async Increment Problem "
comments: true
category: Design

---

### Question

[link](http://www.careercup.com/question?id=18315663)

> If two threads are incrementing a variable 100 times each without synchronization, what would be the possible min and maximum value.

### Solution

Well, max is init+200, and min is init+2. Suggested by the [top answer](http://www.careercup.com/question?id=18315663):

1. P1 & P2 copy var 
1. P1 increments 99 times. so var becomes var + 99 
1. P2 increments once. so var becomes var + 1 
1. P1 copies var (value is var + 1) 
1. P2 increments 99 times. so var becomes var + 100 
1. P1 increments once. so var becomes var + 2
