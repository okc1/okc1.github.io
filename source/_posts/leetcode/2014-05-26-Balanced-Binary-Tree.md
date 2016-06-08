---
layout: post
title: "[LeetCode 110] Balanced Binary Tree"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/balanced-binary-tree/)

<div class="question-content">
            <p></p><p>Given a binary tree, determine if it is height-balanced.
</p>

<p>
For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of <i>every</i> node never differ by more than 1.
</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a difficult question for me__. 

My first code contains many dulicate calls. I have posted it below as an illustration of bad example. 

### Solution

The solution should make use of the return value from the recursion, and avoid duplication calls. The standard solution is posted below. 

### Code

__First, my initial solution__. It takes 30ms more than next code. 

    public boolean isBalanced(TreeNode root) {
        // my old code re-submit, for speed test
        if (root == null) return true;
        if (Math.abs(depth(root.left) - depth(root.right)) > 1) {
            return false;
        }
        if (! isBalanced(root.left)) return false;
        if (! isBalanced(root.right)) return false;
        return true;
    }
    
    private int depth(TreeNode node) {
        if (node == null) return 0;
        if (node.left == null) return 1 + depth(node.right);
        if (node.right == null) return 1 + depth(node.left);
        return 1 + Math.max(depth(node.left), depth(node.right));
    }

__Second, the standard solution__

    public boolean isBalanced(TreeNode root) {
        return helper(root) != -1;
    }
    
    private int helper(TreeNode node) {
        if (node == null) return 0;
        int a = helper(node.left);
        if (a == -1) return -1;
        int b = helper(node.right);
        if (b == -1) return -1;
        if (Math.abs(a - b) <= 1) 
            return Math.max(a, b) + 1;
        else return -1;
    }
