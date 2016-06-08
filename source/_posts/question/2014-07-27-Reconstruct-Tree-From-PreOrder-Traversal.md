---
layout: post
title: "[Question] Reconstruct Tree From Pre-Order Traversal"
comments: true
category: Question
tags: [ src ]
---

### Question 

[link](http://tech-queries.blogspot.sg/2011/06/reconstruct-tree-from-pre-order.html)

> A tree has a special property where leaves are represented with ‘2’ and non-leaf with ‘1’. Each node has either 0 or 2 children. If given preorder traversal of this tree, construct the tree. 

> Example: Given Pre Order string => 12122, output: 

           1
          / \
         2   1
            / \
           2   2

### Analysis

> [In normal scenario](http://tech-queries.blogspot.sg/2011/06/reconstruct-tree-from-pre-order.html), it’s not possible to detect where left subtree ends and right subtree starts using only pre-order traversal. But here, we are given a special property. Since every node has either 2 children or no child, we can surely say that if a node exists then its sibling also exists.

Keep a public variable and build the tree recursively until the list finishes. 

### Code

	ListNode list = null; // this is the input list public variable
    
    public TreeNode main(ListNode input) {
        list = input;
        return constructTree();
    }

	private TreeNode constructTree() {
		if (list == null) {
			return null;
		}
		TreeNode root = new TreeNode(list.val);
		list = list.next;

		if (root.val == 1) {
			root.left = constructTree();
			root.right = constructTree();
		}
		return root;
	}
