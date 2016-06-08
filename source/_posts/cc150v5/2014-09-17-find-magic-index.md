---
layout: post
title: "[CC150v5] 9.3 Find Magic Index "
comments: true
category: CC150v5
tags: [ src ]
---

### Question 1 

> A magic index in an array A[l.. .n-l] is defined to be an index such that A[i] = i. 

> Given a sorted array of distinct integers, write a method to find a magic index, if one exists, in array A. 

### Question 2 

> FOLLOW UP: What if the values are not distinct? 

### Solution

__This is a difficult binary search question__! 

__Question 1 is slightly easier__: we simplyl use binary search, and we are able to discard half of the array each time. 

1. if (array[mid] > mid), then we discard the right half.
1. if (array[mid] < mid), then we discard the left half.

__Question 2 is difficult__. We cannot discard half of the input any more. Instead, we discard a range between (mid) and (array[mid]). Then check left and right part seperately. 

So, I wrote the following code:

	int mid = left + (right - left) / 2;
	if (array[mid] == mid) {
		return mid;
	} else {
		int smaller = Math.min(array[mid], mid);
		int larger = Math.max(array[mid], mid);
		int leftResult = helper(array, left, smaller);
		if (leftResult != -1) {
			return leftResult;
		} else {
			return helper(array, larger, right);
		}
	}

This becomes an endless loop. We did not discard point 'mid' in the code above. The correct code is posted below. 

### Code

__code for non-duplicate input__

	public static int myAnswerNonDup(int[] array) {
		int len = array.length;
		return helper(array, 0, len - 1);
	}

	public static int helper(int[] array, int left, int right) {
		if (right < left) {
			return -1;
		}
		int mid = left + (right - left) / 2;
		if (array[mid] == mid) {
			return mid;
		} else if (array[mid] < mid) {
			// discard all element to the left of array[mid]
			return helper(array, mid + 1, right);
		} else {
			return helper(array, left, mid - 1);
		}
	}

__code for have-duplicate input__

	public static int myAnswerWithDup(int[] array) {
		int len = array.length;
		return helper(array, 0, len - 1);
	}

	public static int helper(int[] array, int left, int right) {
		if (right < left) {
			return -1;
		}
		int mid = left + (right - left) / 2;
		if (array[mid] == mid) {
			return mid;
		} else {
			int smaller = 0;
			int larger = 0;
			if (array[mid] < mid) {
				smaller = array[mid];
				larger = mid + 1;
			} else if (array[mid] > mid) {
				smaller = mid - 1;
				larger = array[mid];
			}
			int leftResult = helper(array, left, smaller);
			if (leftResult != -1) {
				return leftResult;
			} else {
				return helper(array, larger, right);
			}
		}
	}
