---
layout: post
title: "[CC150v4] 4.5 Find Next Node in BST "
comments: true
category: CC150v4

---

### Question

> Write an algorithm to find the ‘next’ node (i.e., in-order successor) of a given node in a binary search tree where each node has a link to its parent. 

### Solution

1. __If current node have a right child__, return the leftmost leaf of right child. 

1. __If current node have no right child__: 

    1. If current is parent's left child, then return parent node. 
    
    1. If current is parent's right child, look all the way up until find a right-turning parent. 
    
    1. If all parent is not right-turning. Return null. 

### Code

__written by me__

	public static TreeNode inorderSucc(TreeNode e) {
		if (e == null)
			return null;
		if (e.right != null) {
			TreeNode p = e.right;
			while (p.left != null) {
				p = p.left;
			}
			return p;
		} else {
			TreeNode p = e.parent;
			while (p != null && p.right == e) {
				e = p;
				p = e.parent;
			}
			return p;
		}
	}
