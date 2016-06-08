---
layout: post
title: "[LeetCode 111] Minimum Depth of Binary Tree"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/minimum-depth-of-binary-tree/)

<div class="question-content">
            <p></p><p>Given a binary tree, find its minimum depth.</p>

<p>The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="white">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__There are various ways to solve this question.__

Eg. DFS, BFS, queue and so on.

### Solution

I have nothing to say with the code. 

### Code

    public int minDepth(TreeNode root) {
        if (root == null) return 0;
        return helper(root, Integer.MAX_VALUE, 1);
    }
    
    private int helper(TreeNode node, int min, int level) {
        if (node == null || level >= min) 
            return min;
        if (node.left == null && node.right == null)
            return level;
        min = helper(node.left, min, level + 1);
        min = helper(node.right, min, level + 1);
        return min;
    }

__Updated on June 10th, this question is better solved with the Divide & Conquer template__! [link](http://answer.ninechapter.com/solutions/minimum-depth-of-binary-tree/)

    public int minDepth(TreeNode root) {
        if (root == null) {
			return 0;
		}
		return checkLeaf(root);
    }
	
	private int checkLeaf(TreeNode node) {
	    if (node == null) {
	        return Integer.MAX_VALUE;
	    }
		if (node.left == null && node.right == null) {
			return 1;
		}
		int ll = checkLeaf(node.left);
		int rr = checkLeaf(node.right);
		return 1 + Math.min(ll, rr);
	}
