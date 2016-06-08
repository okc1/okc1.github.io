---
layout: post
title: "[Question] Union and Intersection of two Linked Lists"
comments: true
category: Question

---


### Question 

[link](http://www.geeksforgeeks.org/union-and-intersection-of-two-linked-lists/)

> Given two Linked Lists, create union and intersection lists that contain union and intersection of the elements present in the given lists. Order of elments in output lists doesn’t matter.
>
> Example:
>
> Input: "10->15->4->20" and "8->4->2->10"
>
> Intersection: 4->10
>
> Union: 2->8->20->4->15->10

### Analysis 

There are 2 solutions. 

First solution is to do mergesort, then do a linear search. Time complexity is O(mlgm + nlgn).

Second solution is using hashing. On time [complexity](http://www.geeksforgeeks.org/union-and-intersection-of-two-linked-lists/): 

> Time complexity of this method depends on the hashing technique used and the distribution of elements in input lists. In practical, this approach may turn out to be better than above method. 
