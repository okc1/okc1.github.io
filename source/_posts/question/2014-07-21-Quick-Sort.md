---
layout: post
title: "[Question] Quick Sort"
comments: true
category: Question
tags: [ src ]
---

### Question 

[link](http://www.programcreek.com/2012/11/quicksort-array-in-java/)

> Quicksort is a divide and conquer algorithm. It first divides a large list into two smaller sub-lists and then recursively sort the two sub-lists. If we want to sort an array without any extra space, Quicksort is a good option. On average, time complexity is O(n log(n)).

### Solution

This question is not easy. Practise more! 

### Code

	public static void quickSortRan(int[] arr, int low, int high) {
		if (low >= high) {
			return;
		}
		int pivot = arr[low + (high - low) / 2];
		int left = low;
		int right = high;
		while (left < right) {
			while (arr[left] < pivot) {
				left++;
			}
			while (arr[right] > pivot) {
				right--;
			}
			if (left <= right) {
				int temp = arr[left];
				arr[left] = arr[right];
				arr[right] = temp;
				left++;
				right--;
			}
		}
		quickSortRan(arr, low, right);
		quickSortRan(arr, left, high);
	}
