---
layout: post
title: "[Question] Check Power of 2"
comments: true
category: Question

---

### Question 

> Requirement: O(1) time

### Solution

Do a special handle for input = 0. [source](http://stackoverflow.com/a/600306)

    bool IsPowerOfTwo(ulong x) {
        return (x & (x - 1)) == 0;
    }
