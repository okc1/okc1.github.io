---
layout: post
title: "[LeetCode 144] Binary Tree Preorder Traversal"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/binary-tree-preorder-traversal/)

<div class="question-content bg-color bg-img font-color">
            <p class="font-color"></p><p class="font-color">Given a binary tree, return the <i>preorder</i> traversal of its nodes' values.</p>

<p class="font-color">
For example:<br>
Given binary tree <code>{1,#,2,3}</code>,<br>
</p><pre>   1
    \
     2
    /
   3
</pre>
<p class="font-color"></p>
<p class="font-color">
return <code>[1,2,3]</code>.
</p>

<p class="font-color"><b>Note:</b> Recursive solution is trivial, could you do it iteratively?</p><p class="font-color"></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is the easiest question of this series__.

In-order and post-order are not easy at all! 

### Code

    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> ans = new LinkedList<Integer>();
        if (root == null) return ans;
        Stack<TreeNode> stack = new Stack<TreeNode>();
        stack.push(root);
        while (!stack.isEmpty()) {
            TreeNode cur = stack.pop();
            ans.add(cur.val);
            // should it do reversely, right?
            if (cur.right != null) stack.push(cur.right);
            if (cur.left != null) stack.push(cur.left);
        }
        return ans;
    }
