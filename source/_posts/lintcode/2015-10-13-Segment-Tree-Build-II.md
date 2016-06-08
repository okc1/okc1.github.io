---
layout: post
title: "[LintCode] Segment Tree Build II "
description: ""
category: LintCode

---

### Question 

[link](http://www.lintcode.com/en/problem/segmemt-tree-build-ii/)

> The structure of Segment Tree is a binary tree which each node has two attributes start and end denote an segment / interval.

> start and end are both integers, they should be assigned in following rules:

> The root's start and end is given by build method.
The left child of node A has start=A.left, end=(A.left + A.right) / 2.
The right child of node A has start=(A.left + A.right) / 2 + 1, end=A.right.
if start equals to end, there will be no children for this node.

> Implement a build method with a given array, so that we can create a corresponding segment tree with every node value represent the corresponding interval max value in the array, return the root of this segment tree.

### Solution

Similar.

### Code

    /**
     * Definition of SegmentTreeNode:
     * public class SegmentTreeNode {
     *     public int start, end, max;
     *     public SegmentTreeNode left, right;
     *     public SegmentTreeNode(int start, int end, int max) {
     *         this.start = start;
     *         this.end = end;
     *         this.max = max
     *         this.left = this.right = null;
     *     }
     * }
     */
    public class Solution {
        /**
         *@param A: a list of integer
         *@return: The root of Segment Tree
         */
        public SegmentTreeNode build(int[] A) {
            if (A == null || A.length == 0) {
                return null;
            }
            return helper(A, 0, A.length - 1);
        }

        private SegmentTreeNode helper(int[] A, int start, int end) {
            if (start > end) {
                return null;
            }
            SegmentTreeNode node = new SegmentTreeNode(start, end);
            if (start == end) {
                node.max = A[start];
                return node;
            } else {
                node.left = helper(A, start, (start + end) / 2);
                node.right = helper(A, (start + end) / 2 + 1, end);
                if (node.right != null) {
                    node.max = Math.max(node.left.max, node.right.max);
                } else {
                    node.max = node.left.max;
                }
            }
            return node;
        }
    }
