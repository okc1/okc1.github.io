---
layout: post
title: "[LintCode] Segment Tree Modify "
description: ""
category: LintCode

---

### Question 

[link](http://www.lintcode.com/en/problem/segment-tree-modify/#)

> For a Maximum Segment Tree, which each node has an extra value max to store the maximum value in this node's interval.

> Implement a modify function with three parameter root, index and value to change the node's value with [start, end] = [index, index] to the new given value. Make sure after this change, every node in segment tree still has the max attribute with the correct value.

### Solution

It's very similar to __Segment Tree Modify/search__. 

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
         *@param root, index, value: The root of segment tree and 
         *@ change the node's value with [index, index] to the new given value
         *@return: void
         */
        public void modify(SegmentTreeNode root, int index, int value) {
            helper(root, index, value);
        }

        private int helper(SegmentTreeNode node, int target, int val) {
            if (node.start > target || node.end < target) {
                // no update, then just return max as normal
                return node.max;
            } else if (node.start == node.end && node.start == target) {
                node.max = val;
                return val;
            } else {
                // check left and right, and update max value accordingly
                node.max = Math.max(helper(node.left, target, val), 
                                    helper(node.right, target, val));
                return node.max;
            }
        }
    }
