---
layout: post
title: "[LeetCode 106] Construct Binary Tree from Inorder and Postorder"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

<div class="question-content">
            <p></p><p>Given inorder and postorder traversal of a tree, construct the binary tree.</p>

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

__This is exactly the same question as__ "Construct Binary Tree from Preorder and Inorder". 

### Solution

I post the code from [this article](http://www.programcreek.com/2013/01/construct-binary-tree-from-inorder-and-postorder-traversal/). 

### Code

    public TreeNode buildTree(int[] inorder, int[] postorder) {
        int inStart = 0, inEnd = inorder.length-1;
        int postStart =0, postEnd = postorder.length-1;
        return buildTree(inorder, inStart, inEnd, postorder, postStart, postEnd);
    }
 
    public TreeNode buildTree(int[] inorder, int inStart, int inEnd, 
                              int[] postorder, int postStart, int postEnd){
        if(inStart > inEnd || postStart > postEnd)
            return null;
        int rootValue = postorder[postEnd];
        TreeNode root = new TreeNode(rootValue);
        int k=0;
        for(int i=0; i< inorder.length; i++){
            if(inorder[i]==rootValue){
                k = i;
                break;
            }
        }
        root.left = buildTree(inorder, inStart, k-1, 
            postorder, postStart, postStart+k-(inStart+1));
        root.right = buildTree(inorder, k+1, inEnd, 
            postorder, postStart+k-inStart, postEnd-1);
        return root;
    }