---
layout: post
title: "[Question] Max Sum In A 2D Array (sub-matrix) "
comments: true
category: Question
tags: [ src ]
---

### Question 

[link](http://tech-queries.blogspot.sg/2010/05/find-max-sum-in-2d-array.html)

> Given a 2D array, find the maximum sum subarray in it. For example, in the following 2D array, the maximum sum subarray is highlighted with blue rectangle and sum of this subarray is 29.

{% img middle /assets/images/max-sum-2d-matrix.png %}

### Analysis

__Note that this is a difficult(and high-frequency) question__.

Try convert this question to "__max sum in 1D array__" by sum up all numbers in the same column. (we know that in 1D array, the algo runs O(n) time)

There's in total O(n^2) combinations of ways to sum up a column. So the __total time complexity is O(n^3)__. 

### Solution

1. Traverse matrix at row level.

1. have a temporary 1-D array and initialize all members as 0.

1. For each row do following

    1. add value in temporary array for all rows below current row
    1. apply 1-D kadane on temporary array
    1. if your current result is greater than current maximum sum, update.

### Code

__written by me__

	public int maxSum(int[][] A) {
		int m = A.length;
		int n = A[0].length;
		int maxResult = Integer.MIN_VALUE;
		for (int i = 0; i < m; i++) {
			int[] temp = new int[n];
			for (int j = i; j < m; j++) {
				// from row#i to row#(m-1), add the number into temp[]
				for (int k = 0; k < n; k++) {
					temp[k] += A[j][k];
				}
				// find max sum for 1D array
				maxResult = Math.max(maxResult, maxSum(temp));
			}
		}
		return maxResult;
	}

	private int maxSum(int[] B) {
		int sumSoFar = 0;
		int maxSum = Integer.MIN_VALUE;
		for (int i = 0; i < B.length; i++) {
			maxSum = Math.max(maxSum, sumSoFar + B[i]);
			sumSoFar = Math.max(0, sumSoFar + B[i]);
		}
		return maxSum;
	}
