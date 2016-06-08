---
layout: post
title: "[LeetCode 101] Symmetric Tree"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/symmetric-tree/)

<div class="question-content">
            <p></p><p>Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).</p>

<p>
For example, this binary tree is symmetric:
</p><pre>    1
   / \
  2   2
 / \ / \
3  4 4  3
</pre>
<p></p>
<p>
But the following is not:<br>
</p><pre>    1
   / \
  2   2
   \   \
   3    3
</pre>
<p></p>

<p>
<b>Note:</b><br>
Bonus points if you could solve it both recursively and iteratively.
</p>
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
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="white">2 ways to solve</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is an easy one__.

### Solution

I solved it using recursion. 

The non-recursion solution is using 2 stacks (or queues). I did not write it, but the code is posted as well, copied from [this post](https://oj.leetcode.com/discuss/456/recusive-solution-symmetric-optimal-solution-inordertraversal). 

### Code

__First, recursion__

    public boolean isSymmetric(TreeNode root) {
        if (root == null) return true;
        return check(root.left, root.right);
    }
    
    private boolean check(TreeNode left, TreeNode right) {
        if (left == null && right == null) return true;
        if (left == null || right == null) return false;
        if (left.val != right.val) return false;
        return check(left.left, right.right) & check(left.right, right.left);
    }

__Second, non-recursion__

    public boolean isSymmetric(TreeNode root) {
        if (root == null) return true;
        Stack<TreeNode> s1 = new Stack<TreeNode>();
        Stack<TreeNode> s2 = new Stack<TreeNode>();
        s1.push(root.left);
        s2.push(root.right);
        while (!s1.empty() && !s2.empty()) {
            TreeNode n1 = s1.pop();
            TreeNode n2 = s2.pop();
            if (n1 == null && n2 == null) continue;
            if (n1 == null || n2 == null) return false;
            if (n1.val != n2.val) return false;
            s1.push(n1.left);
            s2.push(n2.right);
            s1.push(n1.right);
            s2.push(n2.left);
        }
        return true;
    }
