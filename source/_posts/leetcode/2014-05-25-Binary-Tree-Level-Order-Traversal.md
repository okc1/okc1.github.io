---
layout: post
title: "[LeetCode 102] Binary Tree Level Order Traversal"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/binary-tree-level-order-traversal/)

<div class="question-content">
            <p></p><p>Given a binary tree, return the <i>level order</i> traversal of its nodes' values. (ie, from left to right, level by level).</p>

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
return its level order traversal as:<br>
</p><pre>[
  [3],
  [9,20],
  [15,7]
]
</pre>
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
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="white">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a really classic question__. 

It is not difficult, however, it's important to understand 2 different ways to solve this problem: __DFS and BFS__. 

__The different between Inorder, preorder, postorder and Level-order__ is explained very well in [this post](http://leetcode.com/2010/09/printing-binary-tree-in-level-order.html).

> pre-order, in-order, and post-order tree traversal are called Depth First Search (DFS), since they visit the tree by proceeding deeper and deeper until it reaches the leaf nodes.

> DFS uses a data structure called Stack and is commonly implemented using recursion. If recursion is not allowed, we can simulate the recursion by using iterative method with the help of stack. For example in the question "Binary Search Tree In-Order Traversal", we have a iterative DFS solution using a stack.

> The most natural solution for level-order traversal is Breadth First Search (BFS), since it visits the nodes level by level. BFS requires the use of a data structure called Queue.

__To summarize, Inorder, preorder and postorder is DFS implemented by Stack. Level-order is BFS implemented by Queue__. It is very important to forever make it clear and take it into your grave 60 years later (maybe more, if not less).

One mor thing, [Stack](http://docs.oracle.com/javase/7/docs/api/java/util/Stack.html) is a Java class that inherit from [Vector](http://docs.oracle.com/javase/7/docs/api/java/util/Vector.html). 

> The Vector class implements a growable array of objects. Like an array, it contains components that can be accessed using an integer index. However, the size of a Vector can grow or shrink as needed to accommodate adding and removing items after the Vector has been created. 

> ArrayList is roughly equivalent to Vector, except that it is unsynchronized. 

However, [Queue](http://docs.oracle.com/javase/7/docs/api/java/util/Queue.html) is an interface, not a class. What is the most popular Queue implementation in Java? It is not __PriorityQueue__, it's __LinkedList__! 

### Solution

__As said, level-order is BFS__. The first code posted below is implemented with a queue. A lot of people used 2 queues, which I don't like. 

__Second code is DFS__. This is my initial solution, maybe because I'm more familiar with DFS. 

### Code

__First, BFS code using 1 queue__

    public ArrayList<ArrayList<Integer>> levelOrder(TreeNode root) {
        ArrayList<ArrayList<Integer>> ans = new ArrayList<ArrayList<Integer>>();
        if (root == null) return ans;
        int level = 0;
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        q.add(root);
        while (! q.isEmpty()) {
            ans.add(new ArrayList<Integer>());
            int curSize = q.size();
            for (int i = 0; i < curSize; i ++) {
                TreeNode node = q.remove();
                ans.get(level).add(node.val);
                if (node.left != null) q.add(node.left);
                if (node.right != null) q.add(node.right);
            }
            level ++;
        }
        return ans;
    }

__First code revised__: I do not really need the variable 'level'. 

    public ArrayList<ArrayList<Integer>> levelOrder(TreeNode root) {
        ArrayList<ArrayList<Integer>> ans = new ArrayList<ArrayList<Integer>>();
        if (root == null) return ans;
        Queue<TreeNode> q = new LinkedList<TreeNode>();
        q.add(root);
        while (! q.isEmpty()) {
            ans.add(new ArrayList<Integer>());
            int curSize = q.size();
            for (int i = 0; i < curSize; i ++) {
                TreeNode node = q.remove();
                ans.get(ans.size() - 1).add(node.val);
                if (node.left != null) q.add(node.left);
                if (node.right != null) q.add(node.right);
            }
        }
        return ans;
    }

__Second, DFS code__

    public ArrayList<ArrayList<Integer>> levelOrder(TreeNode root) {
        ArrayList<ArrayList<Integer>> ans = new ArrayList<ArrayList<Integer>>();
        if (root == null) return ans;
        traverse(ans, root, 0);
        return ans;
    }
    
    private void traverse (ArrayList<ArrayList<Integer>> ans, TreeNode node, int level) {
        if (node == null) return;
        if (ans.size() >= level + 1) 
            ans.get(level).add(node.val);
        else {
            ArrayList<Integer> temp = new ArrayList<Integer>();
            temp.add(node.val);
            ans.add(temp);
        }
        traverse(ans, node.left, level + 1);
        traverse(ans, node.right, level + 1);
    }
