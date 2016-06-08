---
layout: post
title: "[LeetCode 124] Binary Tree Maximum Path Sum"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/binary-tree-maximum-path-sum/)

<div class="question-content">
            <p></p><p>
Given a binary tree, find the maximum path sum.
</p>

<p>
The path may start and end at any node in the tree.
</p>

<p>
For example:<br>
Given the below binary tree,
</p><pre>       1
      / \
     2   3
</pre>
<p></p>
<p>
Return <code>6</code>.
</p><p></p>
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

__This is a difficult DFS question__.

The basic idea is: 

> When we are in a root node, how we decided to include current node in the maximum path sum? We need to calculate the depth in both subtree. In the meantime, we need to set a variable "max" to store the max path sum we found during the recursion. 

> Pay attention that when a subtree sum to negative value, we discard this subtree. 

> Otherwise, max path sum including current node is __leftSum + cur.val + rightSum__

> Max depth of current node is __(maximum value of leftSum and rightSum) + cur.val__

### Solution

There are 2 points that may incur problems during coding, they are: 

1. The recursive solution is calculating the 'max height' while checking 'its own max path sum'. It's a bit hard to explain. Basic idea is doing 2 things at same time, while traversing (are one result is returned, another is stored in a public variable, at least for code 1 below). 

2. Note that 'max height' of a child branch can be nagative. In this case, WE MUST SET IT TO 0. 

The first point is a concept seen in previous questions, but I forgot which. The second point is important, because I missed this and got failed a few times without any clue. 

### Code

__First, recursive solution__

    int max = Integer.MIN_VALUE;
    
    public int maxPathSum(TreeNode root) {
        maxHeight(root);
        return max;
    }
    
    private int maxHeight(TreeNode node) {
        if (node == null) return 0;
        int l = Math.max(0, maxHeight(node.left));
        int r = Math.max(0, maxHeight(node.right));
        max = Math.max(max, l + r + node.val);
        return node.val + Math.max(l, r);
    }

__Second, previous code refactored__. 

I removed the global variable, and instead pass an array as reference in the recursion. In this way the 'shared' array achieve same functionality as a global variable. 

    public int maxPathSum(TreeNode root) {
        int[] shared = {Integer.MIN_VALUE};
        maxHeight(root, shared);
        return shared[0];
    }
    
    private int maxHeight(TreeNode node, int[] shared) {
        if (node == null) return 0;
        int l = Math.max(0, maxHeight(node.left, shared));
        int r = Math.max(0, maxHeight(node.right, shared));
        shared[0] = Math.max(shared[0], l + r + node.val);
        return node.val + Math.max(l, r);
    }

__Updated on June 10th, it's a terrible practise to use global variable__. The [new solution](http://answer.ninechapter.com/solutions/binary-tree-maximum-path-sum/) suggested by Mr. Huang uses a new ResultType Class to solve the problem. 

    private class ResultType {
        int singlePath, maxPath;
        ResultType(int singlePath, int maxPath) {
            this.singlePath = singlePath;
            this.maxPath = maxPath;
        }
    }
	
    public int maxPathSum(TreeNode root) {
        ResultType result = helper(root);
        return result.maxPath;
    }
	
	private ResultType helper(TreeNode node) {
	    // null case
	    if (node == null) {
	        return new ResultType(0, Integer.MIN_VALUE);
	    }
	    // divide
	    ResultType ll = helper(node.left);
	    ResultType rr = helper(node.right);
	    // conquer
	    int curSinglePath = Math.max(0, node.val + 
	            Math.max(ll.singlePath, rr.singlePath));
	    int childMaxPath = Math.max(ll.maxPath, rr.maxPath);
	    int curMaxPath = Math.max(childMaxPath, node.val + 
	            ll.singlePath + rr.singlePath);
	    // done
	    return new ResultType(curSinglePath, curMaxPath);
	}
