---
layout: post
title: "[Google] Crazy Distance Between Strings "
comments: true
categories:
- q-google
- z-string-search
tags: [ src ]
---

### Question 

[link](http://stackoverflow.com/questions/15061908/google-interview-find-crazy-distance-between-strings)

> X and Y are strings formed by 0 or 1. Distance is define as: 

    D(X,Y) = Remove chars common at the start from both X & Y. 
    Then add the remaining lengths from both the strings.

> For e.g.

    D(1111, 1000) = Only First alphabet is common. So the remaining string is 111 & 000. Therefore the result length("111") & length("000") = 3 + 3 = 6

> For e.g.

    D(0101, 01100) = Only First two alphabets are common. So the remaining string is 01 & 100. Therefore the result length("01") & length("100") = 2 + 3 = 5

> Now given n input, say like

    1111
    1000
    101
    1100

> Find out the maximum crazy distance between 2 strings.

> __n is__ the number of input strings. __m is__ the max length of any input string. 

### Solution

This is the [source](http://stackoverflow.com/a/15062640). 

> Put the strings into a tree, where 0 means go left and 1 means go right. __O(m*n) time__. 

Example: 

                Root
                 1
              0      1
             0 1*   0  1
            0*     0*    1*

> where the * means that an element ends there. Constructing this tree clearly takes O(n m).

> Now we have to find __the diameter of the tree__ (the longest path between two nodes). 

How to find out longest path between 2 leaf nodes? Please refer to __[Google] Diameter of a Binary Tree__ for explanation.  

Total time complexity is __O(m*n) time__.

### Code

	public int crazyDist(String[] input) {
		TreeNode root = this.buildTree(input);
		return this.findMaxPath(root).path - 1;
	}

	private Result findMaxPath(TreeNode node) {
		if (node == null) {
			return new Result(Integer.MIN_VALUE, 0);
		}
		Result lr = this.findMaxPath(node.left);
		Result rr = this.findMaxPath(node.right);
		int path = Math.max(lr.path, rr.path);
		if (lr.depth != 0 && rr.depth != 0) {
			// this check is important, because if any of the child node is
			// NULL, this root will not be eligible for computing the path
			path = Math.max(path, lr.depth + rr.depth + 1);
			// Why? cuz diameter must go from one leaf, thru root, and reach
			// another leaf. This is different from "Maximum Path Sum" leetcode
		}
		return new Result(path, 1 + Math.max(lr.depth, rr.depth));
	}

	private TreeNode buildTree(String[] input) {
		TreeNode root = new TreeNode(123);
		// share a common root. this root is deducted from the final calculation
		for (String str : input) {
			// insert str under the root
			TreeNode p = root;
			for (char c : str.toCharArray()) {
				if (c == '0') {
					if (p.left == null) {
						p.left = new TreeNode(124);
						// if 0, go to left; otherwise go to right
						// thus value of TreeNodes does not really matter
					}
					p = p.left;
				} else {
					if (p.right == null) {
						p.right = new TreeNode(125);
					}
					p = p.right;
				}
			}
		}
		return root;
	}

	class Result {
		int path;
		int depth;

		public Result(int a, int b) {
			path = a;
			depth = b;
		}
	}
