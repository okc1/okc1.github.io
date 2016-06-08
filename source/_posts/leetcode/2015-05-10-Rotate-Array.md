---
layout: post
title: "[LeetCode 189] Rotate Array "
comments: true
category: Leetcode
---

### Question 

[link](https://leetcode.com/problems/rotate-array/)

<div class="question-content">
              <p></p><p>Rotate an array of <i>n</i> elements to the right by <i>k</i> steps.</p>
<p>For example, with <i>n</i> = 7 and <i>k</i> = 3, the array <code>[1,2,3,4,5,6,7]</code> is rotated to <code>[5,6,7,1,2,3,4]</code>. </p>

<p><b>Note:</b><br>
Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.
</p>

<p class="showspoilers"><a href="#" onclick="showSpoilers(this); return false;">[show hint]</a></p>
<div class="spoilers" style="display: none;"><b>Hint:</b><br>
Could you do it in-place with O(1) extra space?
</div>

<p>Related problem: <a href="/problems/reverse-words-in-a-string-ii/">Reverse Words in a String II</a></p>

<p><b>Credits:</b><br>Special thanks to <a href="https://oj.leetcode.com/discuss/user/Freezen">@Freezen</a> for adding this problem and creating all test cases.</p><p></p>
              
                <div id="tags" class="btn btn-xs btn-warning">Show Tags</div>
                <span class="hide">
                  
                  <a class="btn btn-xs btn-primary" href="/tag/array/">Array</a>
                  
                </span>
              
            </div>

### Solution

This question is very standard "rotate 3 times" solution. 

### Code

    public class Solution {
        public void rotate(int[] nums, int k) {
            if (nums == null || nums.length == 0) {
                return;
            }
            int len = nums.length;
            k = k % len;

            reverse(nums, 0, len - k - 1);
            reverse(nums, len - k, len - 1);
            reverse(nums, 0, len - 1);
        }

        void reverse(int[] nums, int start, int end) {
            while (start < end) {
                int temp = nums[start];
                nums[start] = nums[end];
                nums[end] = temp;
                start++;
                end--;
            }
        }
    }

