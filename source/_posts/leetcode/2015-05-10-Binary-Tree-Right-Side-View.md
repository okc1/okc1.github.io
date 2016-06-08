---
layout: post
title: "[LeetCode 199] Binary Tree Right Side View "
comments: true
category: Leetcode
---

### Question 

[link](https://leetcode.com/problems/binary-tree-right-side-view/)

<div class="question-content">
              <p></p><p>Given a binary tree, imagine yourself standing on the <i>right</i> side of it, return the values of the nodes you can see ordered from top to bottom.</p>

<p>
For example:<br>
Given the following binary tree,<br>
</p><pre>   1            &lt;---
 /   \
2     3         &lt;---
 \     \
  5     4       &lt;---
</pre>
<p></p>
<p>
You should return <code>[1, 3, 4]</code>.
</p>

<p><b>Credits:</b><br>Special thanks to <a href="https://leetcode.com/discuss/user/amrsaqr">@amrsaqr</a> for adding this problem and creating all test cases.</p><p></p>
              
                <div id="tags" class="btn btn-xs btn-warning">Show Tags</div>
                <span class="hide">
                  
                  <a class="btn btn-xs btn-primary" href="/tag/tree/">Tree</a>
                  
                  <a class="btn btn-xs btn-primary" href="/tag/depth-first-search/">Depth-first Search</a>
                  
                  <a class="btn btn-xs btn-primary" href="/tag/breadth-first-search/">Breadth-first Search</a>
                  
                </span>
              
            </div>

### Solution

This question basically is binary tree traversal. During the process, we keep a list and update the elements in it. 

### Code

    /**
     * Definition for a binary tree node.
     * public class TreeNode {
     *     int val;
     *     TreeNode left;
     *     TreeNode right;
     *     TreeNode(int x) { val = x; }
     * }
     */
    public class Solution {
        public List<Integer> rightSideView(TreeNode root) {
            List<Integer> result = new ArrayList<Integer>();
            traverse(result, root, 1);
            return result;
        }

        void traverse(List<Integer> result, TreeNode node, int level) {
            if (node == null) return;
            if (level > result.size()) {
                result.add(node.val);
            }
            traverse(result, node.right, level + 1);
            traverse(result, node.left, level + 1);
        }
    }
