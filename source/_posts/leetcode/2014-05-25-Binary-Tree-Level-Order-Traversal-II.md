---
layout: post
title: "[LeetCode 107] Binary Tree Level Order Traversal II"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/binary-tree-level-order-traversal-ii/)

<div class="question-content">
            <p></p><p>Given a binary tree, return the <i>bottom-up level order</i> traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).</p>

<p>
For example:<br>
Given binary tree <code>{3,9,20,#,#,15,7}</code>,<br>
</p><pre>    3
   / \
  9  20
    /  \
   15   7
</pre>
<p></p>
<p>
return its bottom-up level order traversal as:<br>
</p><pre>[
  [15,7]
  [9,20],
  [3],
]
</pre>
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
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="white">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is the same question as previous one__. 

### Solution

__There are also 2 solution: BFS and DFS__. 

I post BFS code below. Only 2 lines are different: ans.get() and ans.add(). 

### Code

    public ArrayList<ArrayList<Integer>> levelOrderBottom(TreeNode root) {
        ArrayList<ArrayList<Integer>> ans = new ArrayList<ArrayList<Integer>>();
        if (root == null) return ans;
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        q.add(root);
        while (! q.isEmpty()) {
            ans.add(0, new ArrayList<Integer>());
            int curSize = q.size();
            for (int i = 0; i < curSize; i ++) {
                TreeNode node = q.remove();
                ans.get(0).add(node.val);
                if (node.left != null) q.add(node.left);
                if (node.right != null) q.add(node.right);
            }
        }
        return ans;
    }
