---
layout: post
title: "[Question] Count Level in Perfect Binary Tree"
comments: true
category: Question
tags: [ src ]
---

### Question 

[link](http://stackoverflow.com/questions/10721583/how-can-i-calculate-the-level-of-a-node-in-a-perfect-binary-tree-from-its-depth)

> A perfect binary tree, i.e. each node in the tree is either a leaf node, or has two children, and all leaf nodes are on the same level. Each node has an index in depth-first order. 

		  0
		/   \
	  1      4
	 / \    / \
	2   3  5   6

> Given the index (k) of a particular node, calculate its level. 

### Solution

__This is a [magical solution](http://stackoverflow.com/a/10721897)__.  It divides the tree in the middle with number k decrease by 1 each time. 

Beautiful, and hard to understand. 

### Code

__not written by me__.

	public int countLevel(TreeNode root, int k, int n) {
		int level = 0;
		while (k != 0) {
			k--;
			n = (n - 1) / 2;
			k = k % n;
			level++;
		}
		return level + 1;
	}
