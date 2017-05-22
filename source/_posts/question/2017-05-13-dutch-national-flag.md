---
layout: post
title: "[Question] Dutch national flag problem "
comments: true
category: Question
tags: [  ]
---

# Question

[link](https://en.wikipedia.org/wiki/Dutch_national_flag_problem)

> Given an array A[] consisting 0s, 1s and 2s, write a function that sorts A[]. The functions should put all 0s first, then all 1s and all 2s in last.

    Example
    Input = {0, 1, 1, 0, 1, 2, 1, 2, 0, 0, 0, 1};
    Output = {0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 2, 2}

# Solution

3-way sort: http://www.geeksforgeeks.org/3-way-quicksort-dutch-national-flag/

# Code

	public int[] threePointerSort(int[] input) {
		if (input == null || input.length <= 1) {
			return input;
		}

		// left is at the leftmost non-0 position
		// right is at rightmost non-2
		// mid is currently being evaluated (before mid, it's sorted)
		int left = 0, right = input.length - 1;
		int mid = left;
		
		while (mid <= right) {
			if (input[mid] > 1) {
				Common.swap(input, mid, right);
				right--;
			} else if (input[mid] < 1) {
				Common.swap(input, left, mid);
				left++;
				mid++;
			} else {
				mid++;
			}
		}

		return input;
	}
