---
layout: post
title: "[Google] Minimum adjustments "
comments: true
category: q-google

---

### Question 

[link](http://www.careercup.com/question?id=6212066786410496)

> Given an integer array, adjust each integers so that the difference of every adjacent integers are not greater than a given number target. 

> If the array before adjustment is A, the array after adjustment is B, you should minimize the sum of |A[i]-B[i]| 

> Given [1,4,2,3] and target=1, one of the solutions is [2,3,2,3], the minimal adjustment cost is 2.

### Solution 

This is a difficult DP. Now we define 2D array like this: 

> dp[i][j]: the minimal adjust cost on changing A[i] to j

And the equation: 

> dp[i][j] = min{dp[i-1][k] + |j-A[i]|} s.t. |k-j| <= target

Refer to the post by [simon.zhangsm](http://www.careercup.com/question?id=6212066786410496)

### Code

Not written.

Available at [OJ](http://lintcode.com/en/problem/minimum-adjustment-cost/#)
