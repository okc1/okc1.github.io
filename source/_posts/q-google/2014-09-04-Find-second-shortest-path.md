---
layout: post
title: "[Google] Find Second Shortest Path "
comments: true
category: q-google

---

### Question 

[link](http://www.careercup.com/question?id=16922663)

> You are given a graph and an algorithm that can find the shortest path b/w any two nodes. 

> Now you have to find the second shortest path between same two nodes. 

### Solution

From the top answer: 

> __Find the shortest path__ between any two nodes. Let them be A and B. 

> Now to get second shortest path between the same nodes, __remove any one edge that is involved in the shortest path__ between the same nodes and calculate the shortest path. 

> Do the above process for each of the node involved in shortest path and keep track of the minimum second shortest path found.
