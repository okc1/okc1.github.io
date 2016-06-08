---
layout: post
title: "[Question] Reservoir sampling "
comments: true
category: Question

---

[Reservoir sampling](http://en.wikipedia.org/wiki/Reservoir_sampling) is a family of randomized algorithms for randomly choosing k samples from a list of n items, where n is either __a very large number__. Typically n is large enough that the list __doesn’t fit into main memory__. For example, a list of search queries in Google and Facebook.

### Question 

[link](http://www.geeksforgeeks.org/reservoir-sampling/)

> given a big array (or stream) of numbers (to simplify), and we need to write an efficient function to randomly select k numbers where 1 <= k <= n. Let the input array be stream[].

### Solution

__O(n)__ time!

1. Create an array sample[0..k-1] and copy first k items of stream[] to it.

1. Now one by one consider all items from (k+1)th item to nth item.

    1. Generate a random number 'j' from 0 to i where i is index of current item in stream[]. 

    1. If j is in range 0 to k-1, replace sample[j] with stream[i]

### Code

not written
