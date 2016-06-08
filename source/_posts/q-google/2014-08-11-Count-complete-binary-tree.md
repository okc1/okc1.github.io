---
layout: post
title: "[Google] Count Complete Binary Tree"
comments: true
category: q-google
tags: [ ItInt5 ]
---

### Question 

[link](http://www.itint5.com/oj/#4)

> 给定一棵[完全二叉树](http://baike.baidu.com/view/427107.htm)（complete binary tree）的根结点，统计该树的结点总数。

> 提示：使用O(n)的递归算法统计二叉树的结点数是一种显而易见的方法，此题中请利用完全二叉树的性质，想出效率更高的算法。

### Solution

Similar to binary search, O(lgn) complexity. 

The idea is, sum up 1 branch of nodes at a time. Do it recursively. The following code is refactored and written by me. 

### Code

__read it from [here](http://www.itint5.com/discuss/125/%E5%A4%A7%E7%89%9B%E8%AF%B7%E6%8C%87%E7%82%B9%EF%BC%8C%E6%95%B0%E6%8D%AE37%E8%BF%90%E8%A1%8C%E8%B6%85%E6%97%B6%EF%BC%88%E9%99%84%E4%BB%A3%E7%A0%81%EF%BC%89)__

	//使用TreeNodeUtil.getLeftChildNode(TreeNode)获得左儿子结点
	//使用TreeNodeUtil.getRightChildNode(TreeNode)获得右儿子结点
	//使用TreeNodeUtil.isNullNode(TreeNode)判断结点是否为空
	public class CountCompleteBinayTreeNodes {
	    public int countNodes(TreeNode root) {
			if (TreeNodeUtil.isNullNode(root)) {
				return 0;
			}
			int hl = height(TreeNodeUtil.getLeftChildNode(root));
			int hr = height(TreeNodeUtil.getRightChildNode(root));
			if (hl == hr) {
				return (int) Math.pow(2, hl) + countNodes(TreeNodeUtil.getRightChildNode(root));
			} else {
				return (int) Math.pow(2, hr) + countNodes(TreeNodeUtil.getLeftChildNode(root));
			}
	    }
		
		private int height(TreeNode root) {
			int count = 0;
			while (!TreeNodeUtil.isNullNode(root)) {
				root = TreeNodeUtil.getLeftChildNode(root);
				count++;
			}
			return count;
		}
	}
