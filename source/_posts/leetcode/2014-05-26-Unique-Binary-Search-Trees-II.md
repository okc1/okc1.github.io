---
layout: post
title: "[LeetCode 95] Unique Binary Search Trees II"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/unique-binary-search-trees-ii/)

<div class="question-content">
            <p></p><p>Given <i>n</i>, generate all structurally unique <b>BST's</b> (binary search trees) that store values 1...<i>n</i>.</p>

<p>
For example,<br>
Given <i>n</i> = 3, your program should return all 5 unique BST's shown below.

</p><pre>   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
</pre>
<p></p>
<p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a question with standard solution__. 

It looks like difficult, but actually the code is very short.

### Solution

This is my previous solution. Everyone in blogs are having same solution. I mean, every single one of  them, [one example](http://gongxuns.blogspot.sg/2013/01/leetcodeunique-binary-search-trees-ii.html). 

### Code

    public ArrayList<TreeNode> generateTrees(int n) {
        return construct(0, n);
    }
    
    ArrayList<TreeNode> construct(int base, int n) {
		ArrayList<TreeNode> ans = new ArrayList<TreeNode>();
		if (n == 0) ans.add(null);
		for (int cur = 1; cur <= n; cur++) 
			for (TreeNode l : construct(base, cur - 1)) 
				for (TreeNode r : construct(base + cur, n - cur)) {
					TreeNode root = new TreeNode(base + cur);
					root.left = l;
					root.right = r;
					ans.add(root);
				}
		return ans;
	}
