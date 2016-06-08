---
layout: post
title: "[LintCode] Maximum Subarray II"
description: ""
category: LintCode

---

### Question 

[link](http://www.lintcode.com/en/problem/maximum-subarray-ii/)

> Given an array of integers, find two non-overlapping subarrays which have the largest sum. The number in each subarray should be contiguous. Return the largest sum.

> Note The subarray should contain at least one number

> Example For given [1, 3, -1, 2, -1, 2], the two subarrays are [1, 3] and [2, -1, -2] or [1, 3, -1, 2] and [2], they both have the largest sum 7.

### Analysis 

__This is not an easy question__. I thought I have to use DP 2 times: 

1. first time, calculate max sum ending at each point.
1. second time, calculate max sum to the left/right of a point (inclusive but not necessarily ending at current point). 

After a second thought, __the first DP path can be denoted with a single variable__. So there comes the solution below.

### Code

    public int maxTwoSubArrays(ArrayList<Integer> nums) {
        // write your code
        int len = nums.size();
        int[] dp1 = new int[len];
        int[] dp2 = new int[len];
        // dp1[k] denotes the max sum to the left of k (inclusive)
        // dp2[k] denotes the max sum to the right of k (inclusive)
        dp1[0] = nums.get(0);
        int sumSoFar = Math.max(0, nums.get(0));
        for (int i = 1; i < len; i++) {
            sumSoFar += nums.get(i);
            dp1[i] = Math.max(dp1[i - 1], sumSoFar);
            sumSoFar = Math.max(0, sumSoFar);
        }
        dp2[len - 1] = nums.get(len - 1);
        sumSoFar = Math.max(0, nums.get(len - 1));
        for (int i = len - 2; i >= 0; i--) {
            sumSoFar += nums.get(i);
            dp2[i] = Math.max(dp2[i + 1], sumSoFar);
            sumSoFar = Math.max(0, sumSoFar);
        }
        // now for every node, calculate leftMaxSum + rightMaxSum
        int maxSum = Integer.MIN_VALUE;
        for (int i = 0; i < len - 1; i++) {
            maxSum = Math.max(maxSum, dp1[i] + dp2[i + 1]);
        }
        return maxSum;
    }
