---
layout: post
title: "[LeetCode 169] Majority Element "
comments: true
category: Leetcode
---

### Question 

[link](https://leetcode.com/problems/majority-element/)

### Solution

<div class="question-content">
              <p></p><p>Given an array of size <i>n</i>, find the majority element. The majority element is the element that appears more than <code>? n/2 ?</code> times.</p>

<p>You may assume that the array is non-empty and the majority element always exist in the array.</p>

<p><b>Credits:</b><br>Special thanks to <a href="https://oj.leetcode.com/discuss/user/ts">@ts</a> for adding this problem and creating all test cases.</p><p></p>
              
                <div id="tags" class="btn btn-xs btn-warning">Show Tags</div>
                <span class="hide">
                  
                  <a class="btn btn-xs btn-primary" href="/tag/divide-and-conquer/">Divide and Conquer</a>
                  
                  <a class="btn btn-xs btn-primary" href="/tag/array/">Array</a>
                  
                  <a class="btn btn-xs btn-primary" href="/tag/bit-manipulation/">Bit Manipulation</a>
                  
                </span>
              
            </div>

### Analysis

I have already covered this question in [[LintCode] Majority Number]({% post_url /lintcode/2014-06-28-Majority-Number %}). However, I have also discovered __a few other very interesting solution__. Check below. 

### Solution

The best solution is of course the voting algorithm. Read code below. 

Second solution presented by offical answer, is to do sorting: 

    public int majorityElement(int[] num) {
        if (num.length == 1) {
            return num[0];
        }

        Arrays.sort(num);
        return num[num.length / 2];
    }

Third interesting solution is doing bit manipulation. Read [Yanyulin's blog](http://www.yanyulin.info/pages/2014/12/851338983752.html) for more. 

### Code

    public class Solution {
        public int majorityElement(int[] num) {
            if (num == null || num.length == 0) {
                return 0;
            }
            int major = num[0];
            long count = 1;

            for (int i = 1; i < num.length; i++) {
                if (major == num[i]) {
                    count++;
                } else if (count == 0) {
                    major = num[i];
                    count = 1;
                } else {
                    count--;
                }
            }

            return major;
        }
    }
