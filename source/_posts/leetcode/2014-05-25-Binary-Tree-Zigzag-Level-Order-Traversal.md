---
layout: post
title: "[LeetCode 103] Binary Tree Zigzag Level Order Traversal"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/binary-tree-zigzag-level-order-traversal/)

<div class="question-content">
            <p></p><p>Given a binary tree, return the <i>zigzag level order</i> traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).</p>

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
return its zigzag level order traversal as:<br>
</p><pre>[
  [3],
  [20,9],
  [15,7]
]
</pre>
<p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="white">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This question is based on "Binary Tree Level Order Traversal"__. 

Altough this is difficulty level 4, the real difficult part is solving "Binary Tree Level Order Traversal". If that question is solved, only slight modification is needed for this question. 

### Solution

__Instead of using queue__ like in "Binary Tree Level Order Traversal", __this question is solved by using Stack__. And it's not hard to see why. The only additional things to note: 

1. There is no 'single stack solution', we must use __2 stacks__. (because when push, it's pushed to top). 

2. Keep a boolean variable to remember rightToLeft or leftToRight. 

### Code

__First, standard BFS solution__ using 2 stacks. 

    public ArrayList<ArrayList<Integer>> zigzagLevelOrder(TreeNode root) {
        ArrayList<ArrayList<Integer>> ans = new ArrayList<ArrayList<Integer>>();
        if (root == null) return ans;
        Stack<TreeNode> q = new Stack<TreeNode>();
        q.push(root);
        boolean reverse = true;
        while (! q.isEmpty()) {
            ans.add(new ArrayList<Integer>());
            Stack<TreeNode> qq = new Stack<TreeNode>();
            int curSize = q.size();
            for (int i = 0; i < curSize; i ++) {
                TreeNode node = q.pop();
                ans.get(ans.size() - 1).add(node.val);
                if (reverse) {
                    if (node.left != null) qq.push(node.left);
                    if (node.right != null) qq.push(node.right);
                }
                else {
                    if (node.right != null) qq.push(node.right);
                    if (node.left != null) qq.push(node.left);
                }
            }
            q = qq;
            reverse = ! reverse;
        }
        return ans;
    }

__Second, DFS solution written by me__, and yes, I love DFS more. 

    public ArrayList<ArrayList<Integer>> zigzagLevelOrder(TreeNode root) {
        ArrayList<ArrayList<Integer>> ans = new ArrayList<ArrayList<Integer>>();
        helper(ans, root, 1);
        return ans;
    }
    
    private void helper(ArrayList<ArrayList<Integer>> ans, TreeNode node, int level) {
        if (node == null) return;
        if (ans.size() < level) {
            ArrayList<Integer> lv = new ArrayList<Integer>();
            lv.add(node.val);
            ans.add(lv);
        }
        else {
            if (level % 2 == 0) 
                ans.get(level - 1).add(0, node.val);
            else
                ans.get(level - 1).add(node.val);
        }
        helper(ans, node.left, level + 1);
        helper(ans, node.right, level + 1);
    }
