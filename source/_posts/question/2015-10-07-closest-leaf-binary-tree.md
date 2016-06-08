---
layout: post
title: "[Question] Find Cloest Leaf in Binary Tree "
comments: true
category: Question
tags: [  ]
---

### Question

[link](www.geeksforgeeks.org/find-closest-leaf-binary-tree/index.html)

> Given a Binary Tree and a key, find distance of the closest leaf.

> Examples:

              1
            /    \    
           2       3
                 /   \  
                5     6   
               /       \
              7         8
             / \       /
            9  10     11
            
    Closest key to '8' is '11', so distance is 1 for '8'
    Closest key to '3' is '2', so distance is 2 for '3'
    Closest key to '5' is either '9' or '10', so distance is 2 for '5'
    Closest key to '2' is '2' itself, so distance is 0 for '2' 

### Solution

> traverse the given tree in preorder and keep track of ancestors (in a caching data struture, either it's List or an array with a correct pointer)

When we find our target, we do 2 things: 

1. find __closest distance on lower subtrees of current node__.

1. for every ancester, find the __closest distance on lower subtrees__, then add with __distance to ancester__. 

Finally, return the smallest value seen above. 

### Code

Inspired by the code from [G4G](www.geeksforgeeks.org/find-closest-leaf-binary-tree/index.html)

	int answer;

	public int findClosest(TreeNode root, int key) {
		answer = Integer.MAX_VALUE;
		helper(root, key, new ArrayList<TreeNode>());
		return answer;
	}

	private void helper(TreeNode node, int key, List<TreeNode> path) {
		if (node == null) {
			return;
		} else if (node.val != key) {
			path.add(node);
			helper(node.left, key, path);
			helper(node.right, key, path);
			path.remove(path.size() - 1);
		} else {
			// key matches with current node value
			answer = lenToLowerLeaf(node);
			// answer initially = cloest leaf from lower

			int len = path.size();
			for (int i = 0; i < len; i++) {
				// for every ancestor, calculate distance and compare
				int ithToLowerLeaf = lenToLowerLeaf(path.get(i));
				answer = Math.min(answer, (len - i) + ithToLowerLeaf);
			}
		}
	}

	private int lenToLowerLeaf(TreeNode node) {
		if (node == null) {
			return Integer.MAX_VALUE;
		} else if (node.left == null && node.right == null) {
			return 0;
		} else {
			return 1 + Math.min(lenToLowerLeaf(node.left), lenToLowerLeaf(node.right));
		}
	}
