---
layout: post
title: "[Fundamental] Quickselect "
comments: true
categories:
- Fundamental
- z-top-K
tags: [ src ]
---

### Question 

[link](http://www.geeksforgeeks.org/k-largestor-smallest-elements-in-an-array/)

> Find Top k smallest element in an array. 

### Analysis

There're 2 solutions. 

First solution, __use a max-heap__. O(nlgk) time complexity.

Second solution is called __[quickselect](http://www.geekviewpoint.com/java/search/quickselect)__, a type of [selection algorithm](http://en.wikipedia.org/wiki/Selection_algorithm) that's based on quicksort. It's averaging O(n) time, but O(n^2) if pivot selection is poor. The code is posted below. There's also a similar [iterative solution](http://blog.teamleadnet.com/2012/07/quick-select-algorithm-find-kth-element.html). 

To [further optimize this](http://www.isnowfy.com/top-k-number/), we can change the pivot selection method by dividing into k group and find median of each. This is called [Median of medians algorithm](http://en.wikipedia.org/wiki/Median_of_medians). The worst case is O(n) time. And this is the best solution for "Top k" questions. 

### Why quickselect is O(n) time?

It's a very good question to ask. Why O(n)?

Well think about it. Let's assume you always find the pivot that makes you eliminate half of the input. 

__The first run, you would read n elements__. Second time you read half of n, and third time, quarter of n. In the end, you read n + n/2 + n/4 + ... = 2n times. 

Compared to the Heap method to find top K, quick select has its advantage. __Heap top K take O(n lgK) time__. So __when K is pretty large__, quick select might be an better solution. 

### Code 

__quickselect__

	public static void quickSelect1(int[] list, int k) {
		selectHelper1(list, 0, list.length - 1, k);
	}

	public static void selectHelper1(int[] list, int left, int right, int k) {
		int pivotIndex = partition(list, left, right);
		if (pivotIndex == k) {
			return;
		} else if (k < pivotIndex) {
			selectHelper1(list, left, pivotIndex - 1, k);
		} else {
			selectHelper1(list, pivotIndex + 1, right, k);
		}
	}

	private static int partition(int[] list, int left, int right) {
		int pivot = left + (right - left) / 2;
		swap(list, right, pivot);
		for (int i = left; i < right; i++) {
			if (list[i] < list[right]) {
				swap(list, i, left);
				left++;
			}
		}
		swap(list, left, right);
		return left;
	}

__quickselect, iteratively__

	public static int quickSelect2(int[] arr, int k) {
		if (arr == null || arr.length <= k)
			throw new Error();
		int from = 0, to = arr.length - 1;
		// if from == to we reached the kth element
		while (from < to) {
			int r = from, w = to;
			int mid = arr[(r + w) / 2];
			// stop if the reader and writer meets
			while (r < w) {
				if (arr[r] >= mid) { // put the large values at the end
					swap(arr, w, r);
					w--;
				} else { // the value is smaller than the pivot, skip
					r++;
				}
			}
			// if we stepped up (r++) we need to step one down
			if (arr[r] > mid)
				r--;
			// the r pointer is on the end of the first k elements
			if (k <= r) {
				to = r;
			} else {
				from = r + 1;
			}
		}
		return arr[k];
	}
