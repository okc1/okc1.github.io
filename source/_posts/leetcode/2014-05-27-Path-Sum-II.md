---
layout: post
title: "[LeetCode 113] Path Sum II"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/path-sum-ii/)

<div class="question-content">
            <p></p><p>
Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.
</p>

For example:<br>
Given the below binary tree and <code>sum = 22</code>,
<pre>              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
</pre>

<p>
return<br>
</p><pre>[
   [5,4,11,2],
   [5,8,4,5]
]
</pre>
<p></p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="lime">2</td>
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

__This is a standard question__

### Solution

My code is simple DFS. However, the coding part is not easy. Note that value can be negative, and think about when to add result into list. 

Just write it by hand and get an idea of it. 

### Code

    public ArrayList<ArrayList<Integer>> pathSum(TreeNode root, int sum) {
        ArrayList<ArrayList<Integer>> ans = new ArrayList<ArrayList<Integer>>();
        helper(root, sum, new ArrayList<Integer>(), ans);
        return ans;
    }
    
    private void helper(TreeNode node, int total, ArrayList<Integer> list, 
                        ArrayList<ArrayList<Integer>> ans) {
        if (node == null) return;
        list.add(node.val);
        if (node.val == total && node.left == null && node.right == null)
            ans.add(new ArrayList(list));
        helper(node.left, total - node.val, list, ans);
        helper(node.right, total - node.val, list, ans);
        list.remove(list.size() - 1);
    }
