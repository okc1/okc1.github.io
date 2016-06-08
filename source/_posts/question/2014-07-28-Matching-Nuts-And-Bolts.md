---
layout: post
title: "[Question] Matching Nuts And Bolts"
comments: true
category: Question
tags: [  ]
---

### Question 

[link](http://tech-queries.blogspot.sg/2011/01/nuts-and-bolts-algorithm.html)

> You are given a collection of nuts of different size and corresponding bolts. You can choose any nut & any bolt together, from which you can determine whether the nut is larger than bolt, smaller than bolt or matches the bolt exactly. However there is no way to compare two nuts together or two bolts together. Suggest an algorithm to match each bolt to its matching nut. 

### Analysis

Use the idea of quicksort. Find pivot and divide. 

### Solution

1. Take a nut from the nuts pile
1. Divide bolts around it in 2 parts, which are smaller and larger than this.
1. Find a matching bolt to this nut.
1. Divide nuts in 2 parts, which are smaller and larger than matching bolt.

Now we have 2 subsets of Nuts and Bolts. 

At every step, we will be able to divide these piles in 2 halves and reduce complexity by a factor of 2. 

__Average case time complexity will be O(nlogn)__, but O(n^2) when pivot is selection poor. 
