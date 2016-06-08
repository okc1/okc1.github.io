---
layout: post
title: "[Google] Diameter of a Binary Tree "
comments: true
category: q-google

---

### Question 

[link](http://www.geeksforgeeks.org/diameter-of-a-binary-tree/)

> The diameter of a tree (sometimes called the width) is the number of nodes on the longest path between two leaves in the tree. 

{% img middle /assets/images/tree-diameter-1.gif %}

### Solution

This is a similar question to __[LeetCode 124] Binary Tree Maximum Path Sum__. __However there's a significant difference__ which might be overlooked while coding. 

Look at this example: 

         0
           1
            1
           0  1
               1

If we only want to find the max path, that would return result of 5, which is root-to-rightmost-leaf. However, the diameter should be 4, which is the distance between 2 leaf nodes. 

A solution is available for reading [here](http://stackoverflow.com/a/3124575). 

For __[Google] Crazy Distance Between Strings__, there is another special case: {"1", "11", "10"}. The program will not output correct result (1), because this is not really the diameter of a tree, but instead, a max path from a non-leaf to a leaf. I leave this part for you to finish. 

### Code

Refer to __[Google] Crazy Distance Between Strings__ for complete code. 
