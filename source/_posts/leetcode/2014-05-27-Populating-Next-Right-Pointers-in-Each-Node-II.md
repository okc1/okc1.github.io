---
layout: post
title: "[LeetCode 117] Populating Next Right Pointers in Each Node II"
comments: true
category: Leetcode

---

### Question 

[link](https://oj.leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/)

<div class="question-content">
            <p></p><p>Follow up for problem "<i>Populating Next Right Pointers in Each Node</i>".</p>
<p>What if the given tree could be any binary tree? Would your previous solution still work?</p>
<p>
<b>Note:</b>
</p><ul><li>You may only use constant extra space.</li></ul>
<p></p>
<p>
For example,<br>
Given the following binary tree,<br>
</p><pre>         1
       /  \
      2    3
     / \    \
    4   5    7
</pre>
<p></p>
<p>
After calling your function, the tree should look like:<br>
</p><pre>         1 -&gt; NULL
       /  \
      2 -&gt; 3 -&gt; NULL
     / \    \
    4-&gt; 5 -&gt; 7 -&gt; NULL
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
		<td bgcolor="red">4</td>
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

__This is a difficult question__. 

We can of course do a BFS, but that's too simple, and it's not related to previous question, thus __Queue__ is not the answer we're looking for. 

__There are 2 ways to solve this problem, recursively and iteratively__. The 2 solutions are quite different, I will explain them. 

### Solution

__First solution is non-recursion, which is from [this blog](http://rleetcode.blogspot.sg/2014/03/follow-up-for-problem-populating-next.html)__. First we declare a pointer 'cur' that points to a node. We assume the 'next-links' are already built in current level, and our job is to generate the 'next-links' for the next level. 

In order to do that, we need another 2 pointers in the next level (one head and one tail) to keep track of the position till where we have finished building the links. So 'cur' keep traversing thru current level, until it reaches the end. Then, we move 'cur' to the head of next level, and continue the process. 

The coding part is not difficult, __which is not the case for next solution__. 

__Second solution is recursive, and it is written in [this blog](http://fisherlei.blogspot.sg/2012/12/leetcode-populating-next-right-pointers_29.html)__. Same as previous solution, we assume that current level have all 'next-links' ready, and we will build these links for next level. 

The way of getting next link for child nodes is a bit different, but I guess that's fine. The difficult part is __during recursive call, I NEED TO CALL THE RECURSION METHOD FOR RIGHT CHILD FIRST, THEN LEFT CHILD__. The reason is, the links from left child to right child is going to be used in the recursion call. If we do left first, we will have problem getting __current.left.next__ (which in this case, will be null). I spent a terribly long time debugging this error, until I found a great explanation [here](https://oj.leetcode.com/discuss/1942/anyone-helps-to-find-bug-for-my-code). 

> in your code: connect(root->left); connect(root->right);

> which means you first recurs left sub-tree, then right subtree. The problem is the right subtree's next pointers are not processed. So in your example, 9->next should be 1, however, when you traverse the left sub tree, 9's next pointer is still NULL. Your code will think 9 is the end of the third level, so the fourth level's 0 will have its next to be NULL.

### Code

__First, my initial solution making use of queue__. It is around 50ms slower than the other solutions. 

    public void connect(TreeLinkNode root) {
        if (root == null) return;
        LinkedList<TreeLinkNode> list = new LinkedList<TreeLinkNode>();
        list.add(root);
        while (! list.isEmpty()) {
            LinkedList<TreeLinkNode> newList = new LinkedList<TreeLinkNode>();
            while (! list.isEmpty()) {
                TreeLinkNode node = list.remove();
                if (! list.isEmpty()) node.next = list.get(0);
                if (node.left != null) newList.add(node.left);
                if (node.right != null) newList.add(node.right);
            }
            list = newList;
        }
    }

__Second, non-recursion solution__

    public void connect(TreeLinkNode root) {
        TreeLinkNode nextLevelHead = null;
        TreeLinkNode nextLevelTail = null;
        TreeLinkNode cur = root;
        while (cur != null) {
            if (cur.left != null) {
                if (nextLevelHead == null) {
                    nextLevelHead = cur.left;
                    nextLevelTail = cur.left;
                }
                else {
                    nextLevelTail.next = cur.left;
                    nextLevelTail = cur.left;
                }
            }
            if (cur.right != null) {
                if (nextLevelHead == null) {
                    nextLevelHead = cur.right;
                    nextLevelTail = cur.right;
                }
                else {
                    nextLevelTail.next = cur.right;
                    nextLevelTail = cur.right;
                }
            }
            cur = cur.next;
            if (cur == null) {
                cur = nextLevelHead;
                nextLevelHead = null;
                nextLevelTail = null;
            }
        }
    }

__Third, recursive solution__

    public void connect(TreeLinkNode root) {
        if (root == null) return;
        // now find root.next's valid child
        TreeLinkNode n = root.next, nextLevelNext = null;
        while (n != null && nextLevelNext == null) {
            if (n.left != null) {
                nextLevelNext = n.left;
                break;
            }
            if (n.right != null) {
                nextLevelNext = n.right;
                break;
            }
            n = n.next;
        }
        // now nextLevelNext is fetched
        if (root.right != null) 
            root.right.next = nextLevelNext;
        if (root.left != null) 
            root.left.next = root.right == null ? nextLevelNext : root.right;
        // recursion call
        connect(root.right);
        connect(root.left);
    }
