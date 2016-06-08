---
layout: post
title: "[CC150v5] 17.6 Order an Array by Sorting Middle "
comments: true
category: CC150v5
tags: [ src ]
---

### Question

> Given an array of integers, write a method to find indices m and n such that if you sorted elements m through n, the entire array would be sorted. Minimize n-m (that is, find the smallest such sequence).

### Solution

Referring to [this guy](http://www.mitbbs.com/article_t/JobHunting/32772399.html): 

> 1. 找到heading的最长递增序列.
>
> 1. 找到tailing的最长的递增序列.

After that: 

> 1. 用中间部分的min去shrink左边.
>
> 1. 用中间部分的max去shrink右边.

### Code

__written by me__

	public static void findUnsortedSequence(int[] array, int[] ans) {
		int len = array.length;
		ans[0] = 0;
		ans[1] = 0;

		// find increasing sequence on left and on right
		int leftPeak = 0;
		while (leftPeak < len - 1) {
			if (array[leftPeak] < array[leftPeak + 1]) {
				leftPeak++;
			} else {
				break;
			}
		}
		if (leftPeak == len - 1) {
			return;
		}
		int rightBottom = len - 1;
		while (rightBottom > 0) {
			if (array[rightBottom] > array[rightBottom - 1]) {
				rightBottom--;
			} else {
				break;
			}
		}

		// leftPeak and rightBottom are found, now read mid part
		int midMin = Integer.MAX_VALUE;
		int midMax = Integer.MIN_VALUE;
		for (int i = leftPeak; i <= rightBottom; i++) {
			midMin = Math.min(midMin, array[i]);
			midMax = Math.max(midMax, array[i]);
		}

		// find left boudary and right boundary
		int leftBound = leftPeak;
		while (leftBound >= 0) {
			if (array[leftBound] < midMin) {
				break;
			}
			leftBound--;
		}
		int rightBound = rightBottom;
		while (rightBound < len) {
			if (array[rightBound] > midMax) {
				break;
			}
			rightBound++;
		}

		// finish it up
		ans[0] = leftBound + 1;
		ans[1] = rightBound - 1;
	}
