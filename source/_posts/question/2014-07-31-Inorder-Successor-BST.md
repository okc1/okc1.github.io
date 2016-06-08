---
layout: post
title: "[Question] Inorder Successor in Binary Search Tree"
comments: true
category: Question
tags: [ src ]
---

### Question 

[link](http://www.geeksforgeeks.org/inorder-successor-in-binary-search-tree/)

> In Binary Tree, Inorder successor of a node is the next node in Inorder traversal of the Binary Tree. Inorder Successor is NULL for the last node in Inoorder traversal.

> Write a program with: 

> 1. parent pointer provided
> 1. parent pointer not provided

### Solution

__If have parent pointer, it's easy__. Read solution [here](http://tech-queries.blogspot.sg/2010/04/inorder-succesor-in-binary-tree.html) or __[CC150v4] 4.5 Find Next Node in BST__. 

__If no parent pointer, then we make use of the property of BST, can get an O(h) solution__. h is the height. 

A very good solution from [this blog](http://algorithmsandme.blogspot.sg/2013/08/binary-search-tree-inorder-successor.html).

1. Start with root.
2. If the node is given has less than root, then search on left side __and update successor__.
3. If the node is greater than root, then search in right part, __don't update successor__.
4. If we find the node
	1. if the node has right sub tree, then the minimum node on the right sub tree of node is the in-order successor.
	1. otherwise, just return successor

The most important point is: we only update __successor__ during left turn, and don't update during right turn. 

### Code

__written by me__

	public TreeNode inorderSuccessor(TreeNode root, TreeNode target) {
		if (target.right != null) {
			return this.findLeftMost(target.right);
		} else {
			return this.traverse(root, new TreeNode(-1), target);
		}
	}

	private TreeNode traverse(TreeNode cur, TreeNode pre, TreeNode target) {
		if (cur.val == target.val) {
			return pre;
		} else if (cur.val < target.val) {
			cur = cur.right;
			return traverse(cur, pre, target);
		} else {
			pre = cur;
			cur = cur.left;
			return traverse(cur, pre, target);
		}
	}

	private TreeNode findLeftMost(TreeNode node) {
		while (node.left != null) {
			node = node.left;
		}
		return node;
	}
