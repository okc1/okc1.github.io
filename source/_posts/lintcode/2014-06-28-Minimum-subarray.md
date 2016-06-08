---
layout: post
title: "[LintCode] Minimum Subarray"
description: ""
category: LintCode

---

### Question 

[link](http://www.lintcode.com/en/problem/minimum-subarray/)

> Given an array of integers, find the subarray with smallest sum. Return the sum of the subarray.

> Note The subarray should contain at least one integer.

> Example For [1, -1, -2, 1], return -3

### Analysis 

Same as "Max subarray". 

### Code

    public int minSubArray(ArrayList<Integer> nums) {
        // write your code
        if (nums == null || nums.size() == 0) {
            return 0;
        }
        int min = nums.get(0);
        int pre = Math.min(0, nums.get(0));
        for (int i = 1; i < nums.size(); i++) {
            pre += nums.get(i);
            min = Math.min(min, pre);
            pre = Math.min(0, pre);
        }
        return min;
    }
