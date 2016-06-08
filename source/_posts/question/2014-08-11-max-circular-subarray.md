---
layout: post
title: "[ItInt5] Maximum circular subarray sum"
comments: true
category: Question
tags: [ ItInt5 ]
---

### Question 

[link](http://www.itint5.com/oj/#9)

> Given n numbers (both +ve and -ve), arranged in a circle, fnd the maximum sum of consecutive number

### Solution

First pass: find max subarray sum.

Second pass: find min subarray sum, and subtract it from total sum. 

Suggested on [G4G](http://www.geeksforgeeks.org/maximum-contiguous-circular-sum/) 

### Code

__written by me__

    public int maxConsSum2(int[] arr) {
		if (arr == null || arr.length == 0) {
			return 0;
		}
        int soFar = 0;
		int max = 0;
		int totalSum = 0;
		for (Integer i: arr) {
			totalSum += i;
			// totalSum is used in next step
			soFar += i;
			soFar = Math.max(soFar, 0);
			max = Math.max(max, soFar);
		}
		int min = 0;
		// calculate the min subarray
		for (Integer i: arr) {
			soFar += i;
			soFar = Math.min(soFar, 0);
			min = Math.min(min, soFar);
		}
		return Math.max(max, totalSum - min);
    }
