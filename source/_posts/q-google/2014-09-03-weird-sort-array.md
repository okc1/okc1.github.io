---
layout: post
title: "[Google] Weird Sort Array "
comments: true
category: q-google
tags: [ src ]
---

### Question 

[link](http://www.mitbbs.com/article_t0/JobHunting/32772813.html)

> 数组排序， 排成 a1<a2>a3<a4>a5。。。这种形式。

### Solution

__The are 2 solutions__. The easy one is this: 

> sort first, then 把临近的奇数换到偶数(index)上, O(nlog n). 

__There's a great O(n) solution however__, not easy to think: 

> 两两比较相邻数字，把大的数字放到下标为奇数的位置。 O(n). 

### Code

__O(nlgn) solution__

	public void solutionOnlgn(int[] A) {
		// this is a O(nlgn) solution
		Arrays.sort(A);
		for (int i = 2; i < A.length; i += 2) {
			swap(A, i - 1, i);
		}
	}

	private void swap(int[] A, int a, int b) {
		A[a] ^= A[b];
		A[b] ^= A[a];
		A[a] ^= A[b];
	}

__O(n) solution__

	public void solutionOn(int[] A) {
		// this is a O(n) solution
		for (int i = 1; i < A.length; i++) {
			// compare (i)th with (i-1)th, and put the large value
			// at odd-indexed positions
			if ((A[i - 1] < A[i] && i % 2 == 0)
					|| (A[i - 1] > A[i] && i % 2 == 1)) {
				swap(A, i - 1, i);
			}
		}
	}

	private void swap(int[] A, int a, int b) {
		A[a] ^= A[b];
		A[b] ^= A[a];
		A[a] ^= A[b];
	}
