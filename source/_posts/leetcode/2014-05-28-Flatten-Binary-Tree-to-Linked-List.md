---
layout: post
title: "[LeetCode 114] Flatten Binary Tree to Linked List"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/flatten-binary-tree-to-linked-list/)

<div class="question-content">
            <p></p><p>
Given a binary tree, flatten it to a linked list in-place.
</p>

<p>
For example,<br>
Given
</p><pre>         1
        / \
       2   5
      / \   \
     3   4   6
</pre>
<p></p>

The flattened tree should look like:<br>
<pre>   1
    \
     2
      \
       3
        \
         4
          \
           5
            \
             6
</pre>

<div class="spoilers" ><b>Hints:</b>
<p>If you notice carefully in the flattened tree, each node's right child points to the next node of a pre-order traversal.</p>
</div><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
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

### Analysis

__This is a very difficult question__, and there are many solutions. 

### Solution

__Analysis of all solutions (except first one) is found in [this great article](http://n00tc0d3r.blogspot.sg/2013/03/flatten-binary-tree-to-linked-list-in.html)__.

__Solution 1 is my code__, I am make use of a 'pre' pointer in this recursive method. This idea is actually quite good, but is never seen in any other people's blogs. 

__Solution 2 is the most standard recursive solution__. It passes in a node, flatten it and return the last node after it's flattened. So we can flatten root node's left and right node respectively, and then connect it. 

<blockquote cite="http://n00tc0d3r.blogspot.sg/2013/03/flatten-binary-tree-to-linked-list-in.html">
To flatten a binary tree, according to the given example, is to recursively insert the left subtree to the right subtree and append the original right subtree to the end of the left subtree, i.e.<br>
<pre>     root                        root
     /  \            -&gt;            \
  left  right                      left
                                     \
                                    right
</pre>
Since we need to append the original right-tree to the end of the left subtree, we let the recursion function return the last node after flatten.
</blockquote>

I missed "root.left = null" while coding, and it resulted in long long time debugging. I think this is a very silly mistake. 

__Solution 3 is making use of a stack__. I have to say, although I can figure how it works, I am still blur about the thinking process of this entire idea. Which is to say, I can't keep it in mind even after learning it. 

I shall try write this code in the future. 

<blockquote>
We can also solve the problem without recursion.<br>
<br>
To do that, we can use a stack to store all right subtrees when we prune them temporarily, and append each of them back after we go through the corresponding left subtree.<br>
<br>
Basically, given a non-empty tree,<br>
<ul>
<li>if it has left subtree, store the right subtree (if not null) to stack, move the left subtree to right;</li>
<li>if not, append back a subtree from stack to the current node's right;</li>
<li>continue to the right node until finish.</li>
</ul>
</blockquote>

__Solution 4 is what I believe the best solution__. It simple uses while loop to put all nodes in the correct position, without recursion or stack. 

> Each time when we prune a right subtree, we use while-loop to find the right-most leaf of the current left subtree, and append the subtree there.

__Analysis of all solutions (except first one) is found in [this great article](http://n00tc0d3r.blogspot.sg/2013/03/flatten-binary-tree-to-linked-list-in.html)__.

### Code

__First, my solution__, a kind of recursive solution

    public void flatten(TreeNode root) {
        helper(new TreeNode(1234), root);
    }
    
    private TreeNode helper(TreeNode pre, TreeNode node) { 
        // pre cannot be null, this function return the last node of the flatten list
        if (node == null) return pre;
        pre.left = null;
        pre.right = node;
        TreeNode a = node.left;
        TreeNode b = node.right;
        TreeNode temp = helper(node, a);
        return helper(temp, b);
    }

__Second, standard recursive solution__

    public void flatten(TreeNode root) {
        helper(root);
    }
    
    private TreeNode helper(TreeNode root) {
        if (root == null) return null;
        TreeNode oldRight = root.right;
        if (root.left != null) {
            root.right = root.left;
            // I missed this line of code: 
            root.left = null;
            root = helper(root.right);
        }
        if (oldRight != null) {
            root.right = oldRight;
            root = helper(root.right);
        }
        // return value is the last element of the flatten tree
        return root;
    }

__Third, stack non-recursive solution__

	public void flatten(TreeNode root) {
		TreeNode cur = root;
		Stack<TreeNode> rtrees = new Stack<TreeNode>();
		while (cur != null) {
			while (cur.left != null) {
				if (cur.right != null)
					rtrees.push(cur.right);
				cur.right = cur.left;
				cur.left = null;
				cur = cur.right;
			}
			if (cur != null && cur.right == null && !rtrees.isEmpty()) {
				cur.right = rtrees.pop();
			}
			cur = cur.right;
		}
	}

__Fourth, non-stack non-recursive solution__

	public void flatten(TreeNode root) {
		TreeNode cur = root;
		while (cur != null) {
			if (cur.left != null) {
				if (cur.right != null) { // if we need to prune a right subtree
					TreeNode next = cur.left;
					while (next.right != null)
						next = next.right;
					next.right = cur.right;
				}
				cur.right = cur.left;
				cur.left = null;
			}
			cur = cur.right;
		}
	}
