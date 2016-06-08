---
layout: post
title: "[LeetCode 198] House Robber "
comments: true
category: Leetcode
---

### Question 

[link](https://leetcode.com/problems/house-robber/)

<div class="question-content">
              <p></p><p>You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and <b>it will automatically contact the police if two adjacent houses were broken into on the same night</b>.</p>

<p>Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight <b>without alerting the police</b>.</p>

<p><b>Credits:</b><br>Special thanks to <a href="https://oj.leetcode.com/discuss/user/ifanchu">@ifanchu</a> for adding this problem and creating all test cases. Also thanks to <a href="https://oj.leetcode.com/discuss/user/ts">@ts</a> for adding additional test cases.</p><p></p>
              
                <div id="tags" class="btn btn-xs btn-warning">Show Tags</div>
                <span class="hide">
                  
                  <a class="btn btn-xs btn-primary" href="/tag/dynamic-programming/">Dynamic Programming</a>
                  
                </span>
              
</div>

### Solution

DP question. Be careful what the initial values of dp(1) is. You should work this out without a problem! 

### Code

    public class Solution {
        public int rob(int[] num) {
            if (num == null || num.length == 0) {
                return 0;
            } else if (num.length == 1) {
                return num[0];
            }
            int len = num.length;
            int[] dp = new int[len];
            dp[0] = num[0];
            dp[1] = Math.max(num[0], num[1]);
            int max = Math.max(num[0], num[1]);
            for (int i = 2; i < len; i++) {
                dp[i] = Math.max(dp[i - 1], dp[i - 2] + num[i]);
                max = Math.max(max, dp[i]);
            }
            return max;
        }
    }
