---
layout: post
title: "[LeetCode 104] Maximum Depth of Binary Tree"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/maximum-depth-of-binary-tree/)

<div class="question-content">
            <p></p><p>Given a binary tree, find its maximum depth.</p>

<p>The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.</p><p></p>
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
		<td bgcolor="white">1</td>
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

    public int maxDepth(TreeNode root) {
        return helper(root, 0, 1);
    }
    
    private int helper(TreeNode node, int max, int level) {
        if (node == null) return max;
        if (node.left == null && node.right == null)
            return Math.max(max, level);
        max = helper(node.left, max, level + 1);
        max = helper(node.right, max, level + 1);
        return max;
    }
