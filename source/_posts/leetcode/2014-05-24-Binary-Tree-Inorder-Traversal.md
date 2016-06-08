---
layout: post
title: "[LeetCode 94] Binary Tree Inorder Traversal"
comments: true
category: Leetcode

---

### Question 
[link](https://oj.leetcode.com/problems/binary-tree-inorder-traversal/)

<div class="question-content">
            <p></p><p>Given a binary tree, return the <i>inorder</i> traversal of its nodes' values.</p>

<p>
For example:<br>
Given binary tree <code>{1,#,2,3}</code>,<br>
</p><pre>   1
    \
     2
    /
   3
</pre>
<p></p>
<p>
return <code>[1,3,2]</code>.
</p>

<p><b>Note:</b> Recursive solution is trivial, could you do it iteratively?</p>

<p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Solution

__This is a classic AND EXTREMELY IMPORTANT question__. 

Solution is well explained in [this blog](http://leetcode.com/2010/04/binary-search-tree-in-order-traversal.html): 

> First, the current pointer is initialized to the root. Keep traversing to its left child while pushing visited nodes onto the stack. When you reach a NULL node (ie, you've reached a leaf node), you would pop off an element from the stack and set it to current. Now is the time to print current's value. Then, current is set to its right child and repeat the process again. When the stack is empty, this means you're done printing.

### Code

__concise code, hard to think of__

    public ArrayList<Integer> inorderTraversal(TreeNode root) {
        ArrayList<Integer> ans = new ArrayList<Integer>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        TreeNode p = root;
        while (p != null || ! stack.isEmpty()) {
            if (p != null) {
                stack.push(p);
                p = p.left;
            }
            else if (! stack.isEmpty()) {
                TreeNode temp = stack.pop();
                ans.add(temp.val);
                p = temp.right;
            }
        }
        return ans;
    }

__more intuitive code, written by Oct 8th, 2014__

    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> ans = new ArrayList<Integer>();
        if (root == null) {
            return ans;
        }
        
        Stack<TreeNode> stack = new Stack<TreeNode>();
        TreeNode p = root;
        while (p != null) {
            stack.push(p);
            p = p.left;
        }
        while (!stack.isEmpty()) {
            p = stack.pop();
            ans.add(p.val);
            p = p.right;
            while (p != null) {
                stack.push(p);
                p = p.left;
            }
        }
        return ans;
    }
