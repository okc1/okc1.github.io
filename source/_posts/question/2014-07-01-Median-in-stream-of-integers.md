---
layout: post
title: "[Question] Median in a stream of integers"
comments: true
category: Question
tags: [ unit test needed ]
---

### Question 

[link](http://www.geeksforgeeks.org/median-of-stream-of-integers-running-integers/)

> Given that integers are read from a data stream. Find median of elements read so for in efficient way. 

> For simplicity assume there are no duplicates. For example, let us consider the stream 5, 15, 1, 3 … The stream of output is 5, 10, 1, 4 …

### Solution

> we can use a max heap on left side to represent elements that are less than effective median, and a min heap on right side to represent elements that are greater than effective median.
>
> After processing an incoming element, the number of elements in heaps differ utmost by 1 element. [source](http://www.geeksforgeeks.org/median-of-stream-of-integers-running-integers/)

So we know that java.util.PriorityQueue is a max-heap. The only question is, how to implement a min-heap? [Someone sugests](http://stackoverflow.com/a/1098454) writing your own customized Comparator: 

> you use two instances of a java.util.PriorityQueue containing the same elements? The first instance would be passed a comparator which puts the maximum at the head, and the second instance would use a comparator which puts the minimum at the head.

### Code

skipped
