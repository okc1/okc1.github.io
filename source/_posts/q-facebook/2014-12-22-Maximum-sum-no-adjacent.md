---
layout: post
title: "[Facebook] Maximum sum such that no two elements are adjacent "
comments: true
category: q-facebook
tags: [ src ]
---

### Question 

[link](http://www.geeksforgeeks.org/maximum-sum-such-that-no-two-elements-are-adjacent/)

> Given an array of positive numbers, find the maximum sum of a subsequence that no 2 numbers should be adjacent. 

> Eg. (3, 2, 7, 10) should return 13 (3+10) 

> Eg. (3, 2, 5, 10, 7) should return 15 (3+5+7).

### Solution

It is an modified version of "max sum subsequence". Answer given on [gfg](http://www.geeksforgeeks.org/maximum-sum-such-that-no-two-elements-are-adjacent/) is: 

> Loop for all elements in arr[] and maintain two sums 'incl' and 'excl' where: 

> incl = Max sum including the previous element 
>
> excl = Max sum excluding the previous element

### Code

__written by me__

	public int solve(int[] A) {
		if (A == null || A.length == 0) {
			return 0;
		} else if (A.length == 1) {
			return A[0];
		} else if (A.length == 2) {
			return Math.max(A[0], A[1]);
		}

		// prePreMax is the max non-adjacency sequence ending 2 position ahead
		// preMax is the max non-adjacency sequence ending 1 position ahead
		int prePreMax = A[0];
		int preMax = A[1];
		int ans = 0;

		for (int i = 2; i < A.length; i++) {
			ans = Math.max(ans, prePreMax + A[i]);
			// set the 2 variables: prePreMax, preMax
			int temp = preMax;
			preMax = Math.max(0, prePreMax + A[i]);
			prePreMax = Math.max(prePreMax, temp);
		}
		return ans;
	}
