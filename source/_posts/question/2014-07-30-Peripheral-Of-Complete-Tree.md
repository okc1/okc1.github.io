---
layout: post
title: "[Question] Peripheral Of A Complete Tree"
comments: true
category: Question

---

### Question 

[link](http://tech-queries.blogspot.sg/2010/09/peripheral-boundary-of-complete-tree.html)

> Write a program to find the anti-clock-wise peripheral (boundary) of a complete tree. 

> For a complete tree peripheral (boundary) is defined as

    1. First the root
    1. Then nodes on left edge
    1. Then leaf nodes
    1. Then nodes on right edge

{% img middle /assets/images/peripheral-of-tree.png %}

> For the above tree, peripheral will be: 0 1 3 7 8 9 10 11 12 13 14 6 2

### Solution

__It's a very tricky solution__. Very clever I would say. 

1. print root node
1. print left nodes and leafs of left subtree in same order
1. print leafs and right nodes of right subtree in same order

Do practise this question again in the future! 

### Code

__written by me__

I used an Enum in the code. 

	public enum PeriType {
		LEFT, RIGHT, LEAF
	}

	private void peripheral(TreeNode root) {
		printNode(root);
		helper(root.left, PeriType.LEFT);
		helper(root.right, PeriType.RIGHT);
		System.out.println();
	}

	private void helper(TreeNode node, PeriType type) {
		if (node == null) {
			return;
		}
		switch (type) {
		case LEFT:
			printNode(node);
			helper(node.left, PeriType.LEFT);
			helper(node.right, PeriType.LEAF);
			break;
		case RIGHT:
			helper(node.left, PeriType.LEAF);
			helper(node.right, PeriType.RIGHT);
			printNode(node);
			break;
		case LEAF:
			if (node.left == null && node.right == null) {
				printNode(node);
			} else {
				helper(node.left, PeriType.LEAF);
				helper(node.right, PeriType.LEAF);
			}
			break;
		}
	}

	private void printNode(TreeNode root) {
		System.out.print(root.val + " ");
	}
