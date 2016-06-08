---
layout: post
title: "[Google] Arithmetic Progression Triplet "
comments: true
category: q-google
tags: [ src ]
---

### Question 

[link](http://www.geeksforgeeks.org/length-of-the-longest-arithmatic-progression-in-a-sorted-array/)

> Given a sorted set, find if there exist three elements in Arithmetic Progression or not. 

### Solution

__This is a rather simple Arithmetic Progression question__. 

> [To find the three elements](http://www.geeksforgeeks.org/length-of-the-longest-arithmatic-progression-in-a-sorted-array/), we first fix an element as middle element and search for other two (one smaller and one greater). 

O(n^2) time. 

### Code

__written by me__

	public boolean longest(int[] A) {
		int len = A.length;
		for (int i = 1; i < len - 1; i++) {
			int left = i - 1;
			int right = i + 1;
			while (left >= 0 && right < len) {
				int total = A[left] + A[right];
				if (total > 2 * A[i]) {
					left--;
				} else if (total < 2 * A[i]) {
					right++;
				} else {
					return true;
				}
			}
		}
		return false;
	}
