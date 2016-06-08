---
layout: post
title: "[Google] Find Nearest Point in a 2D Space"
comments: true
category: q-google
tags: [ unit test needed ]
---

### Question 

[link](http://www.careercup.com/question?id=5634947435986944)

> You are given information about hotels in a country/city. X and Y coordinates of each hotel are known. You need to suggest the list of nearest hotels to a user who is querying from a particular point (X and Y coordinates of the user are given). Distance is calculated as the straight line distance between the user and the hotel coordinates. 

### Solution

__Build a 2-D Tree (by using Binary Tree)__. 

First find the root, then divide the rest of nodes by left-side and right-side. Then, divide by up-side and down-side. 

There's a very good example video [here](http://www.youtube.com/watch?v=T9h2KKJ_Pl8), which talked about how to construct a 2-D tree. 

After this __preprocessing__, the search for nearest hotels in about O(lgn). However, if we were to return a list of nearest nodes, I've got no idea. 
