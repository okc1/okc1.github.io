---
layout: post
title: "[Google] Postorder successor in Binary Tree"
comments: true
category: q-google

---

### Question 

[link](http://www.careercup.com/question?id=5173972006076416)

> Write an algorithm to find the ‘next’ post-order successor of a given node in a binary tree and binary search tree.

> 1. where each node has a link to its parent. 
> 1. without parent pointer 

> Implement 2 versions of the algorithm: 1.) binary tree 2.) BST

### Solution

In postorder, any node below current node shall be 'predecessor' of current node. Thus we only care about current node's parent. 

Suggested by a user: 

    1) parent pointer is given. 
    - go to the parent of the current node. 
    - if current node is the right child of its parent => print parent. 
    - else return leftmost node of the right sub-tree of parent. 

    2) parent pointer is not given. 
    - traverse the tree and find the parent of the current node 
    - do the same as method (1). 
