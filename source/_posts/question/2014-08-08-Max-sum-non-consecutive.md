---
layout: post
title: "[Question] Max Sum Of Non-Consecutive Elements"
comments: true
category: Question
tags: [ src ]
---

### Question 

[link](http://tech-queries.blogspot.sg/2009/05/max-possible-sum-of-non-consecutive.html)

> There is an integer array consisting positive numbers only. 

> Find maximum possible sum of elements such that there are no 2 consecutive elements present in the sum.

### Solution

It's a little tricky to write the equation. Always remember the __basic principle of DP__ is to assume that solution is found for (i -1), and then we calculate solution for input (i). 

__Don't miss the (i-1) part__. 

### Code

__written by me__

	public int maxSumNonConsec(int[] input) {
		int len = input.length;
		int[] dp = new int[len];
		dp[0] = input[0];
		dp[1] = Math.max(input[0], input[1]);
		for (int i = 2; i < len; i++) {
			dp[i] = Math.max(dp[i - 1], input[i] + dp[i - 2]);
		}
		return dp[len - 1];
	}
