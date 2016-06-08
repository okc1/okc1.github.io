---
layout: post
title: "[Design] Median of array in Distributed Computers"
comments: true
category: Design

---

### Question

[link](http://www.quora.com/Distributed-Algorithms/What-is-the-distributed-algorithm-to-determine-the-median-of-arrays-of-integers-located-on-different-computers)

> What is the __distributed algorithm__ to determine the median of arrays of 1 billion integers located on different computers?

### Solution

1. Suppose you have __a master node__ (or are able to use a consensus protocol to elect a master from among your servers).

1. The master queries all servers for the size of their sets of data, so that it knows to look for the k = n/2 largest element.

1. The master then selects a random server and queries __a random element__. 

1. The master broadcasts this element to each server. 

1. Each server partitions its elements into those larger than or equal to the broadcasted element and those smaller than the broadcasted element.

1. Each server returns to the master the __size of the larger-than partition__, call this m. 

    1. If the sum of these sizes is greater than k, the master indicates to each server to disregard the 'less-than' set. 
    
    1. If it is less than k, the master indicates to disregard the larger-than sets and updates k = k - m.  
    
    1. If it is exactly k, the algorithm terminates and the value returned is the pivot selected at the beginning of the iteration.

1. Recurse beginning with selecting a new random pivot from the remaining elements.

[ref](http://qr.ae/k2DcS)
