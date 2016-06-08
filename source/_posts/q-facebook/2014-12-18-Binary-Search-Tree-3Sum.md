---
layout: post
title: "[Facebook] Binary Search Tree 3Sum "
comments: true
category: q-facebook
tags: [ src ]
---

### Question 

DLL - [link](http://www.geeksforgeeks.org/find-if-there-is-a-triplet-in-bst-that-adds-to-0/)

Inorder - [link](http://www.geeksforgeeks.org/find-a-pair-with-given-sum-in-bst/)

> Given a BST, write a function that returns true if there is a triplet that sums to 0, returns false otherwise. 

### Solution

We will solve the question just like we do __[LeetCode 15] 3Sum__. What is missing is an random access of tree nodes.

In fact, we do not need random access. Tree traversal (one after another in sequence) would be good enough. 

Now there're 2 solution. __First is to convert the tree to Double-linked list__, then do 3Sum. The conversion takes O(n) time and O(logn) extra space, and 3Sum take O(n^2). however doing this modifies the original tree. 

__Second solution is to to inorder traversal and reversed inorder traversal__. For me, this solution is preferred. Time and space used is same. 

### Code

__DLL way, written by me__ 

	public void findTriplet(TreeNode root, int target) {
		TreeNode[] dll = convertToDll(root);
		TreeNode head = dll[0];
		TreeNode tail = dll[1];
		// note that the bst inorder dll should already in sorted by value
		TreeNode first = head;
		while (first.right != null) {
			TreeNode left = first.right;
			TreeNode right = tail;
			while (left.val < right.val) {
				int diff = first.val + left.val + right.val - target;
				if (diff == 0) {
					System.out.println("Found triplet: " + first.val + " "
							+ left.val + " " + right.val + " for sum of "
							+ target);
				}
				if (diff <= 0) {
					left = left.right;
				}
				if (diff >= 0) {
					right = right.left;
				}
			}
			first = first.right;
		}
	}

	private TreeNode[] convertToDll(TreeNode node) {
		TreeNode[] ans = new TreeNode[2];
		// do the left side of node
		if (node.left == null) {
			ans[0] = node;
		} else {
			TreeNode[] preAns = convertToDll(node.left);
			ans[0] = preAns[0];
			node.left = preAns[1];
			preAns[1].right = node;
		}
		// do the right side of node
		if (node.right == null) {
			ans[1] = node;
		} else {
			TreeNode[] postAns = convertToDll(node.right);
			ans[1] = postAns[1];
			node.right = postAns[0];
			postAns[0].left = node;
		}
		return ans;
	}

__inorder way__ - basically is just __iterator of binary tree__. 
