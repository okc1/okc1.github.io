---
layout: post
title: "[LeetCode 105] Construct Binary Tree from Preorder and Inorder"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

<div class="question-content">
            <p></p><p>Given preorder and inorder traversal of a tree, construct the binary tree.</p>

<p><b>Note:</b><br>
You may assume that duplicates do not exist in the tree.
</p><p></p>
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
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is an interesting question__. 

The key is, __the tree header is always the first element in the pre-order traversal__. Knowing this is enough to help us divide the lists and solve the question recursively. 

__About time complexity__. According to the [analysis](http://leetcode.com/2011/04/construct-binary-tree-from-inorder-and-preorder-postorder-traversal.html), it is O(nlgn) if the tree is balance, and O(n^2) if the tree is totally skewed. This article suggests using HashTable for searching, which achieves O(n) efficiency. 

> We left out some details on how we search the root value’s index in the inorder sequence. How about a simple linear search? If we assume that the constructed binary tree is always balanced, then we can guarantee the run time complexity to be O(N log N), where N is the number of nodes. However, this is not necessarily the case and the constructed binary tree can be skewed to the left/right, which has the worst complexity of O(N2). I quote the entire article below. 

> A more efficient way is to eliminate the search by using an efficient look-up mechanism such as hash table. By hashing an element’s value to its corresponding index in the inorder sequence, we can do look-ups in constant time. Now, we need only O(N) time to construct the tree, which theoretically is the most efficient way.

### Solution

I post my code below. However, a better code is written in [this post](http://edwardliwashu.blogspot.sg/2013/01/construct-binary-tree-from-preorder-and.html). 

### Code

__First, my code__, it's 100ms slower than next code. 

    public TreeNode buildTree(int[] preorder, int[] inorder) {
        int len = preorder.length;
        if (len == 0) return null;
        TreeNode root = new TreeNode(preorder[0]);
        int leftLen = 0;
        while (inorder[leftLen] != preorder[0]) leftLen++;
        int[] leftPreOrder = new int[leftLen];
        int[] rightPreOrder = new int[len - 1 - leftLen];
        int[] leftInOrder = new int[leftLen];
        int[] rightInOrder = new int[len - 1 - leftLen];
        for (int i = 1; i <= leftLen; i ++) {
            leftPreOrder[i-1] = preorder[i];
            leftInOrder[i-1] = inorder[i-1];
        }
        for (int i = leftLen + 1; i < len; i ++) {
            rightPreOrder[i-leftLen-1] = preorder[i];
            rightInOrder[i-leftLen-1] = inorder[i];
        }
        root.left = buildTree(leftPreOrder, leftInOrder);
        root.right = buildTree(rightPreOrder, rightInOrder);
        return root;
    }

__Second, other ppl's code__

	public TreeNode buildTree(int[] preorder, int[] inorder) {
		int preLength = preorder.length;
		int inLength = inorder.length;
		return buildTree(preorder, 0, preLength - 1, inorder, 0, inLength - 1);
	}

	public TreeNode buildTree(int[] pre, int preStart, int preEnd, int[] in,
			int inStart, int inEnd) {
		if (inStart > inEnd) return null;
		int rootVal = pre[preStart];
		int rootIndex = 0;
		for (int i = inStart; i <= inEnd; i++) {
			if (in[i] == rootVal) {
				rootIndex = i;
				break;
			}
		}
		int len = rootIndex - inStart;
		TreeNode root = new TreeNode(rootVal);
		root.left = buildTree(pre, preStart + 1, preStart + len, in, inStart,
				rootIndex - 1);
		root.right = buildTree(pre, preStart + len + 1, preEnd, in,
				rootIndex + 1, inEnd);
		return root;
	}
