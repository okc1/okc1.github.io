---
layout: post
title: "[Testing] Random error debugging 1 "
comments: true
category: Testing

---

### Question 

[link](http://stackoverflow.com/questions/4531742/debugging-a-program-that-crashes-10-times-in-different-places)

> You are given the source to an application which is crashing during run time. After running it 10 times in a debugger, you find it never crashes in the same place. 

> What programming errors could be causing this crash? How would you test each one?

### Analysis

1. code depends on __system time or RNG__

1. disk full, i.e. other processes may delete a different file causing more space to be available

1. memory issue, i.e. other processes allocate and/or free memory

1. a pointer points to a random location in memory that is changed by another process causing some values be "valid" (very rare though)

[In general](http://stackoverflow.com/a/4531769) a situation __with other process__ is likely.
