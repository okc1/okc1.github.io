---
layout: post
title: "[Question] Axis Aligned Rectangles "
comments: true
category: Question

---

### Question

[link](http://ankitsambyal.blogspot.sg/2013/10/finding-overlapping-rectangles-in-given.html), MIT handouts Person_A

> Describe an algorithm that takes an unsorted array of axis-aligned rectangles and returns __any pair of__ rectangles that overlaps, if there is such a pair. 

> Axis-aligned means that all the rectangle sides are either parallel or perpendicular to the x- and y-axis. 

> Each rectangle object has two variables: the x-y coordinates of the upper-left corner and the bottom-right corner.

### Analysis

A lot of different solutions on the internet, [example 1](http://www.quora.com/Algorithms/Given-a-set-of-n-axis-aligned-rectangles-in-the-plane-find-how-big-is-the-largest-subset-of-these-rectangles-that-contain-a-common-point-in-O-n-3-and-then-in-order-O-nlogn) and [example 2](http://ankitsambyal.blogspot.sg/2013/10/finding-overlapping-rectangles-in-given.html), and some questions asks you to return all overlapping pairs. For now, we just return __any pair__ that overlaps. 

### Solution 

I concluded some solution and come up with this (the idea of BST is covered in the end of [this pdf](http://www.cs.princeton.edu/~rs/AlgsDS07/17GeometricSearch.pdf)): 

1. Sort the input by left edge. 
1. One by one, get one rectangle from the sorted input, and make a pair (rect.top, rect.bottom). 
1. Insert this pair into a __Interval Search Tree__. 
1. This tree is a BST, and use first value of the pair as BST key. 
1. Insert pair at the correct BST location. If conflicts, we've found 1 overlapping pair. 

The code for searching a intersect, and insert a pair looks like this: 

    Node x = root;
    while (x != null) {
        if (x.interval.intersects(lo, hi)) 
            return x.interval;
        else if (x.left == null)  x = x.right;
        else if (x.left.max < lo) x = x.right;
        else                      x = x.left;
    }
    return null;
