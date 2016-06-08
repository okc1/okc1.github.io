---
layout: post
title: "[CC150v5] 17.13 Convert BST to DLL "
comments: true
category: CC150v5
tags: [ src ]
---

### Question

> Consider a simple node-like data structure called BiNode, which has pointers to two other nodes.

    public class BiNode {
        public BiNode node1, node2;
        public int data;
    }

> The data structure BiNode could be used to represent both a binary tree (where node1 is the left node and node2 is the right node) or a doubly linked list (where node1 is the previous node and node2 is the next node). Implement a method to convert a binary search tree (implemented with BiNode) into a doubly linked list. The values should be kept in order and the operation should be performed in place (that is, on the original data structure). 

### Solution

At another post __[LeetCode Plus] Convert BST to Circular DLL__, we already discussed 2 approaches: 

1. in-order traversal approach
1. divide and conquer approach

First approach isn't intuitive. We will further discuss D&C approach here. 

__The key of the solution is how we return both HEAD and TAIL__. The book suggests 3 ways: 

1. Build a __data structure__ to store both head and tail
1. __Just return head__, and retrieve tail by traversing thru - bad time complexity O(n^2)
1. __Use circular linked-list__! Time O(n). 

I wrote the code for 1st and 2nd approach. And 3rd is already covered in previous post. 

* You need to understand why we need the list to be circular. 

### Code

__Approach 1__

	public static BiNode convert(BiNode root) {
		BiNodePair res = helper(root);
		return res.leftMost;
	}

	private static BiNodePair helper(BiNode node) {
		if (node == null) {
			return null;
		}
		BiNodePair res = new BiNodePair(node, node);
		if (node.node1 != null) {
			BiNodePair leftRes = helper(node.node1);
			res.leftMost = leftRes.leftMost;
			leftRes.rightMost.node2 = node;
			node.node1 = leftRes.rightMost;
		}
		if (node.node2 != null) {
			BiNodePair rightRes = helper(node.node2);
			res.rightMost = rightRes.rightMost;
			rightRes.leftMost.node1 = node;
			node.node2 = rightRes.leftMost;
		}
		return res;
	}

	static class BiNodePair {
		BiNode leftMost;
		BiNode rightMost;

		public BiNodePair(BiNode node1, BiNode node2) {
			leftMost = node1;
			rightMost = node2;
		}
	}

__Approach 2__

	public static BiNode convert(BiNode root) {
		if (root == null) {
			return null;
		}
		return helper(root);
	}

	private static BiNode helper(BiNode node) {
		// node is not null
		BiNode newHead = node;
		// do left part
		if (node.node1 != null) {
			newHead = helper(node.node1);
			BiNode leftTail = getListTail(newHead);
			leftTail.node2 = node;
			node.node1 = leftTail;
		}
		// do right part
		if (node.node2 != null) {
			BiNode rightHead = helper(node.node2);
			node.node2 = rightHead;
			rightHead.node1 = node;
		}
		return newHead;
	}

	private static BiNode getListTail(BiNode head) {
		// head is not null
		while (head.node2 != null) {
			head = head.node2;
		}
		return head;
	}
