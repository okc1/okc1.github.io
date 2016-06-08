---
layout: post
title: "[Question] Count multiples of array "
comments: true
category: Question

---

### Question 

[link](http://www.mitbbs.com/article_t/JobHunting/32882735.html)

> N是一个很大的正整数——可能到10^15次方，

> 简单起见，不考虑溢出，或者假设用python

> A 是一个array，里面存着一些正整数，up to 1000个

> 从1 - N这N个数，有多少个数，不能被A中的任何一个数整除的？

### Solution

It's a very difficult question. 

We can't do it like a Sieve of Eratosthenes, cuz N is too large. The best solution is at [this post](http://www.mitbbs.com/article_t/JobHunting/32882735.html), level 9: 

Consider the simplest case: A={2}, then any odd number below N is OK, so the result would be (N - N/2). Then consider A={2, 3}, any number below N that is not mutiply of 2 or 3 is OK, so the result would be (N - N/2 - N/3 + N/6). Then consider A={2, 3, 5}, __the result would be (N - N/2 - N/3 - N/5 + N/6 
+ N/10 + N/15 - N/30)__. 

So there is a general rule: 

for A={a1, a2, ..., aN}, if ai is not dividable by aj for any i != j, then we could:

1. for i from 1 to N, calc r1 = N - SUM(N/ai);
2. for i, j from 1 to N, i != j, calc r2 = r1 + SUM(N/(ai*aj));
3. for i, j, k from 1 to N, i != j != k, calc r3 = r2 - SUM(N/(ai*aj*ak));
4. ...
5. until all numbers in A are chosen.
6. then the final rN is the result.

So for the problem, first we preprocess A to __eliminate any multiplies in A__. For example, A={2, 4, 5}, we can eliminate 4 because it is a mutiply of 2 which is also in A. So A'={2, 5}, then we calc:

r1 = 10 - 10/2 - 10/5 = 10 - 5 - 2 = 3;
r2 = r1 + 10/10 = 3 + 1 = 4;

then the final result is 4.

Refer to __[Question] Multiples of 3 and 5__.

### Code

not written
