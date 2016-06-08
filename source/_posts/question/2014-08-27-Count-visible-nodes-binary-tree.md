---
layout: post
title: "[Twitter] Count Visible Nodes in Binary Tree"
comments: true
category: Question
tags: [ src ]
---

### Question 

[link](http://codesays.com/2014/solution-to-count-visible-nodes-in-binary-tree/)

>  In a binary tree, if in the path from root to the node A, there is no node with greater value than A’s, this node A is visible. We need to count the number of visible nodes in a binary tree. For example, in the following tree:

			5
		 /     \
	   3        10
	  / \      /
	20   21   1

> There are four (4) visible nodes: 5, 20, 21, and 10.

### Solution

This is an easy question. A solution is available [here](http://codesays.com/2014/solution-to-count-visible-nodes-in-binary-tree/). 

### Code

__written by me__

	public int countVisible(TreeNode root) {
		return helper(root, Integer.MIN_VALUE);
	}

	private int helper(TreeNode node, int ancesterMax) {
		if (node == null) {
			return 0;
		}
		int newMax = Math.max(ancesterMax, node.val);
		if (node.val > ancesterMax) {
			return 1 + helper(node.left, newMax) + helper(node.right, newMax);
		} else {
			return helper(node.left, newMax) + helper(node.right, newMax);
		}
	}
