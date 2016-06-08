---
layout: post
title: "[LeetCode 173] Binary Search Tree Iterator "
comments: true
category: Leetcode
---

### Question 

[link](https://leetcode.com/problems/binary-search-tree-iterator/)

<div class="question-content">
              <p></p><p>Implement an iterator over a binary search tree (BST). Your iterator will be initialized with the root node of a BST.</p>

<p>Calling <code>next()</code> will return the next smallest number in the BST.</p>

<p><b>Note: </b><code>next()</code> and <code>hasNext()</code> should run in average O(1) time and uses O(<i>h</i>) memory, where <i>h</i> is the height of the tree. </p>

<p><b>Credits:</b><br>Special thanks to <a href="https://oj.leetcode.com/discuss/user/ts">@ts</a> for adding this problem and creating all test cases.</p><p></p>
              
                <div id="tags" class="btn btn-xs btn-warning">Show Tags</div>
                <span class="hide">
                  
                  <a class="btn btn-xs btn-primary" href="/tag/tree/">Tree</a>
                  
                  <a class="btn btn-xs btn-primary" href="/tag/stack/">Stack</a>
                  
                </span>
              
            </div>

### Analysis

This is an extremely important question, if you are going for an interview. I repeat: __this is an extremely important question, if you are going for an interview__. If you do not remember it by heart, I will repeat again. 

The solution of the iterator applies to a lot of related questions. So make sure you practise this question until you are perfect. You WILL BE ASKED this question at times. 

You could read my other post [[Question] Iterator of Binary Search Tree]({% post_url /question/2014-06-14-Iterator-of-Tree %}). 

### Solution

We only need to keep 1 variable in RAM, that is a stack. 

### Code

    public class BSTIterator {

        Stack<TreeNode> stack = new Stack<TreeNode>();

        public BSTIterator(TreeNode root) {
            while (root != null) {
                stack.push(root);
                root = root.left;
            }
        }

        /** @return whether we have a next smallest number */
        public boolean hasNext() {
            return !stack.isEmpty();
        }

        /** @return the next smallest number */
        public int next() {
            if (!hasNext()) {
                return 0;
            }
            TreeNode next = stack.pop();
            TreeNode node = next.right;
            while (node != null) {
                stack.push(node);
                node = node.left;
            }
            return next.val;
        }
    }
