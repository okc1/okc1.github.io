---
layout: post
title: "[LeetCode 145] Binary Tree Postorder Traversal"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/binary-tree-postorder-traversal/)

<div class="question-content bg-color bg-img font-color">
            <p class="font-color"></p><p class="font-color">Given a binary tree, return the <i>postorder</i> traversal of its nodes' values.</p>

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
return <code>[3,2,1]</code>.
</p>

<p class="font-color"><b>Note:</b> Recursive solution is trivial, could you do it iteratively?</p><p class="font-color"></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

Unlike pre-order traversal, __this is a very difficult question__.

### Solution

__First, I wrote the solution using a HashSet, and it works__. However, this solution is not good because it uses some space. 
For more generalized way to write DFS code, read another post __Implement DFS using a Stack__. 

__The best and most popular solution is proposed by [1337c0d3r](http://leetcode.com/2010/10/binary-tree-post-order-traversal.html)__. It basically uses 1 more pointer to track the current status (whether I'm traversing down, or up, and in which direction etc.). The extra pointer is called 'prev'. 

> We use a prev variable to keep track of the previously-traversed node. Let’s assume curr is the current node that’s on top of the stack. When prev is curr‘s parent, we are traversing down the tree. In this case, we try to traverse to curr‘s left child if available (ie, push left child to the stack). If it is not available, we look at curr‘s right child. If both left and right child do not exist (ie, curr is a leaf node), we print curr‘s value and pop it off the stack.

> If prev is curr‘s left child, we are traversing up the tree from the left. We look at curr‘s right child. If it is available, then traverse down the right child (ie, push right child to the stack), otherwise print curr‘s value and pop it off the stack.

> If prev is curr‘s right child, we are traversing up the tree from the right. In this case, we print curr‘s value and pop it off the stack.

Referring to his code, I wrote the 2nd piece of code below and it works. 

__Amazingly, that code can be simplified, which becomes the 3rd code__ (I thought it won't pass at first). The way that code got simplified is by keeping current pointer steady, so that the 2 pointers can meet. Altough program logic is exactly same, this interesting code is worth reading. 

### Code

__First, my solution using HashSet__

    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> ans = new LinkedList<Integer>();
        Stack<TreeNode> stack = new Stack<TreeNode>();
        if (root != null) stack.push(root);
        HashSet<TreeNode> visited = new HashSet<TreeNode>();
        while (!stack.isEmpty()) {
			TreeNode cur = stack.pop();
			if (visited.contains(cur))
				ans.add(cur.val);
			else {
				stack.push(cur);
				visited.add(cur);
				if (cur.right != null) stack.push(cur.right);
				if (cur.left != null) stack.push(cur.left);
			}
        }
        return ans;
    }

__Second, using 2 pointers__

    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> ans = new LinkedList<Integer>();
        if (root == null) {
			return ans;
		}
		Stack<TreeNode> stack = new Stack<TreeNode>();
        stack.push(root);
        TreeNode pre = null, cur = null;
		while (!stack.isEmpty()) {
			cur = stack.peek();
			if (pre == null || pre.left == cur || pre.right == cur) {
				if (cur.left == null && cur.right == null) {
					ans.add(stack.pop().val);
				}
				else if (cur.left != null) {
					stack.push(cur.left);
				}
				else if (cur.right != null) {
					stack.push(cur.right);
				}
			}
			else if (cur.left == pre) {
				if (cur.right != null) {
					stack.push(cur.right);
				}
				else {
					ans.add(stack.pop().val);
				}
			}
			else if (cur.right == pre) {
				ans.add(stack.pop().val);
			}
			pre = cur;
		}
        return ans;
    }

__Third, simplified version of 2nd code__

__Commented on June 10th__: Note that 'pre' and 'cur' are never going to be apart for more then 1 edge (they can overlap) 

    public List<Integer> postorderTraversal(TreeNode root) {
		List<Integer> result = new ArrayList<Integer>();
		Stack<TreeNode> stack = new Stack<TreeNode>();
		TreeNode prev = null; // previously traversed node
		TreeNode curr = root;
		if (root == null) {
			return result;
		}
		stack.push(root);
		while (!stack.empty()) {
			curr = stack.peek();
			if (prev == null || prev.left == curr || prev.right == curr) {
            // traverse down the tree
				if (curr.left != null) {
					stack.push(curr.left);
				} else if (curr.right != null) {
					stack.push(curr.right);
				}
			} else if (curr.left == prev) {
            // traverse up the tree from the left
				if (curr.right != null) {
					stack.push(curr.right);
				}
			} else if (curr.right == prev || curr == prev){
            // traverse up the tree from the right
            // or at a leaf point
				result.add(curr.val);
				stack.pop();
			}
			prev = curr;
		}
		return result;
	}
