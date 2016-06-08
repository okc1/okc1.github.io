---
layout: post
title: "[LeetCode 154] Find Minimum in Rotated Sorted Array II "
comments: true
category: Leetcode
---

### Question 

[link](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array-ii/)

<div class="question-content">
              <p></p><blockquote>
<p><i>Follow up</i> for "Find Minimum in Rotated Sorted Array":<br>
What if <i>duplicates</i> are allowed?</p>

<p>Would this affect the run-time complexity? How and why?</p>
</blockquote>

<p>Suppose a sorted array is rotated at some pivot unknown to you beforehand.</p>

<p>(i.e., <code>0 1 2 4 5 6 7</code> might become <code>4 5 6 7 0 1 2</code>).</p>

<p>Find the minimum element.</p>

<p>The array may contain duplicates.</p><p></p>
              
                <div id="tags" class="btn btn-xs btn-warning">Show Tags</div>
                <span class="hide">
                  
                  <a class="btn btn-xs btn-primary" href="/tag/array/">Array</a>
                  
                  <a class="btn btn-xs btn-primary" href="/tag/binary-search/">Binary Search</a>
      about/            
                </span>
              
            </div>

### Solution

This question is simply a modified version of previous question. The special cases of the input makes it O(n) worst case complexity. 

### My Code

    public class Solution {
        public int findMin(int[] num) {
            if (num == null || num.length == 0) {
                return 0;
            }
            return helper(num, 0, num.length - 1);
        }

        private int helper(int[] num, int left, int right) {
            if (num[left] < num[right] || left == right) {
                return num[left];
            } else if (num[left] == num[right]) {
                return helper(num, left + 1, right);
            } else if (left + 1 == right) {
                return num[right];
            }
            int mid = left + (right - left) / 2;
            if (num[mid] >= num[left]) {
                return helper(num, mid, right);
            } else {
                return helper(num, left, mid);
            }
        }
    }
