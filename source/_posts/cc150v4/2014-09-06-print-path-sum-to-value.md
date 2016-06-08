---
layout: post
title: "[CC150v4] 4.8 Print Path Sum to Value "
comments: true
category: CC150v4

---

### Question

> You are given a binary tree in which each node contains a value. Design an algorithm to print all paths which sum up to that value. Note that it can be any path in the tree - it does not have to start at the root. 

### Solution

__Keep a list of items as buffer__, and check the following condition: 

> “does this node complete a path with the sum?”

There're n nodes in total, and the max size of buffer is lg(n), so the time complexity is O(nlgn). 

### Code

__written by me__

	public static void find(TreeNode head, int target) {
		findSum(head, target, new ArrayList<Integer>());
	}

	private static void findSum(TreeNode node, int target, List<Integer> buffer) {
		if (node == null)
			return;

		buffer.add(node.data);
		int sum = 0;
		for (int i = buffer.size() - 1; i >= 0; i--) {
			sum += buffer.get(i);
			if (sum == target) {
				// from (i)th element until the last element is a valid path
				printPath(buffer, i);
			}
		}

		List<Integer> clone1 = new ArrayList<Integer>(buffer);
		findSum(node.left, target, clone1);

		List<Integer> clone2 = new ArrayList<Integer>(buffer);
		findSum(node.right, target, clone2);
	}

	private static void printPath(List<Integer> buffer, int start) {
		System.out.print("Path: ");
		for (int i = start; i < buffer.size(); i++) {
			System.out.print(buffer.get(i) + " ");
		}
		System.out.println();
	}
