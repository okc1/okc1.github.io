---
layout: post
title: "[LeetCode 98] Validate Binary Search Tree"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/validate-binary-search-tree/)

<div class="question-content">
            <p></p><p>
Given a binary tree, determine if it is a valid binary search tree (BST).
</p>

<p>
Assume a BST is defined as follows:
</p><ul>
<li>The left subtree of a node contains only nodes with keys <b>less than</b> the node's key.</li>
<li>The right subtree of a node contains only nodes with keys <b>greater than</b> the node's key.</li>
<li>Both the left and right subtrees must also be binary search trees.</li>
</ul>
<p></p>
<p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a textbook-like example of recursion__. 

I solved it using DFS, but there is actually a much more concise solution. 

### Code

__First, my code__, it's basically a in-order traversal. 

    int num = Integer.MIN_VALUE;
    
    public boolean isValidBST(TreeNode root) {
        if (root == null) return true;
        if(! isValidBST(root.left)) return false;
        if (num >= root.val) return false;
        num = root.val;
        if(! isValidBST(root.right)) return false;
        return true;
    }

__Second, great solution I found from [this post](http://www.programcreek.com/2012/12/leetcode-validate-binary-search-tree-java/)__

	public static boolean isValidBST(TreeNode root) {
	    return validate(root, Integer.MIN_VALUE, Integer.MAX_VALUE);
	}

	public static boolean validate(TreeNode root, int min, int max) {
	    if (root == null) return true;
	    if (root.val <= min || root.val >= max)
	        return false;
	    return validate(root.left, min, root.val) 
        	&& validate(root.right, root.val, max);
	}
