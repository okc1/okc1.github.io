---
layout: post
title: "[LintCode] Segment Tree Query "
description: ""
category: LintCode

---

### Question 

[link](http://www.lintcode.com/en/problem/segment-tree-query/)

> For an integer array (index from 0 to n-1, where n is the size of this array), in the corresponding SegmentTree, each node stores an extra attribute max to denote the maximum number in the interval of the array (index from start to end).

> Design a query method with three parameters root, start and end, find the maximum number in the interval [start, end] by the given root of segment tree.

### Solution

Slightly difficult as we need to keep in mind the following: 

1. what's the return condition? (start and end is large enough to cover the entire range)

1. how to handle overlapping case? (find min-point first and then analyse case by case)

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
         *@param root, start, end: The root of segment tree and 
         *                         an segment / interval
         *@return: The maximum number in the interval [start, end]
         */
        public int query(SegmentTreeNode root, int start, int end) {
            // write your code here
            if (root == null || start > end) {
                return -1;
            } else if (root.start > end || root.end < start) {
                return -1;
            } else if (root.start >= start && root.end <= end) {
                return root.max;
            }
            int mid = (root.start + root.end) / 2;
            return Math.max(query(root.left, start, Math.min(mid, end)), 
                            query(root.right, Math.max(mid + 1, start), end));
        }
    }
