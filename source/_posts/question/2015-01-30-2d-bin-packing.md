---
layout: post
title: "[Question] 2D Bin Packing "
comments: true
category: Question

---

### Question 

[link](http://en.wikipedia.org/wiki/Bin_packing_problem)

> Objects of different volumes must be packed into a finite number of bins or containers each of volume V in a way that minimizes the number of bins used.

{% img middle /assets/images/bin-packing.png %}

### Solution

Explanation from [here](http://stackoverflow.com/a/8765049): 

1. Build a binary tree. Each branch in the tree contains a sprite. 
1. Each __leaf node represents available space__. 
1. Initially the tree has just the root node, which represents all available space. 
1. To add a sprite to the tree, search the tree for an unoccupied (leaf) node __big enough__ to hold the sprite. 
1. Turn that node from a leaf into a branch by setting the sprite as the node's occupant and giving the node two children. 
1. One child represents the remaining space to the right of the sprite; 
1. the other represents the remaining space below the sprite and the first child.

For detailed implementation and code, refer to [this](http://codeincomplete.com/posts/2011/5/7/bin_packing/) comprehensite guide. BTW, it's used for __auto generating CSS Sprites__ which puts images into a large graph. 
