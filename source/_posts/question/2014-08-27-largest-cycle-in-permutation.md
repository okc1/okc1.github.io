---
layout: post
title: "[Twitter] Largest Cycle in Permutation "
comments: true
category: Question

---

### Question 

[link](http://get-that-job-at-google.blogspot.sg/2013/01/twitter-programming-test.html)

> Given a permutation which contains numbers in the range [1, N], return the length of the largest cycle in the permutation. 

> A [permutation cycle](http://mathworld.wolfram.com/PermutationCycle.html) is a subset of a permutation whose elements trade places with one another. 

> Sample Testcases:

> a) longestCycle([2 3 1]) returns 3, since only cycle is (1 2 3) whose length is 3

> b) longestCycle([5 4 3 2 1]) returns 2, since the permutation can be decomposed into (1 5), (2 4), (3) 

### Solution

This is just an idea. 

Now first of all, its important to understand __what is a cycle in permutation__. 

Keeping that in mind, I take (5,4,3,2,1) as an example. First, we fetch 5, and we swap number 5 with the 5th element of the array (which is 1). After this swap, value 1 is in the 1st position, so this cycle is done, the length is 2. 

We continue doing this until __all numbers of value v is in the (v)th position__, we should know the largest length of cycle during this process. 

I did not write code, and I found very little relevant resources. If you did, please leave a comment below. 
