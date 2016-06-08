---
layout: post
title: "[LintCode] Segment Tree Query II "
description: ""
category: LintCode

---

### Question 

[link](http://www.lintcode.com/en/problem/segment-tree-query-ii/)

> For an array, we can build a SegmentTree for it, each node stores an extra attribute count to denote the number of elements in the the array which value is between interval start and end. (The array may not fully filled by elements)

> Design a query method with three parameters root, start and end, find the number of elements in the in array's interval [start, end] by the given root of value SegmentTree.

### Solution

Similar.

### Code

    /**
     * Definition of SegmentTreeNode:
     * public class SegmentTreeNode {
     *     public int start, end, count;
     *     public SegmentTreeNode left, right;
     *     public SegmentTreeNode(int start, int end, int count) {
     *         this.start = start;
     *         this.end = end;
     *         this.count = count;
     *         this.left = this.right = null;
     *     }
     * }
     */
    public class Solution {
        /**
         *@param root, start, end: The root of segment tree and 
         *                         an segment / interval
         *@return: The count number in the interval [start, end]
         */
        public int query(SegmentTreeNode root, int start, int end) {
            if (root == null || start > end) {
                return 0;
            } else if (root.start > end || root.end < start) {
                return 0;
            } else if (start <= root.start && root.end <= end) {
                return root.count;
            }
            int mid = (root.start + root.end) / 2;
            return query(root.left, start, Math.min(mid, end)) + 
                    query(root.right, Math.max(mid + 1, start), end);
        }
    }
