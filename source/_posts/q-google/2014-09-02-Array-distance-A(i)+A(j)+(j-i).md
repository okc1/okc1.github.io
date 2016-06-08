---
layout: post
title: "[Google] Array Distance A(i)+A(j)+(j-i) "
comments: true
category: q-google
tags: [ src ]
---

### Question 

[link](http://www.mitbbs.com/article/JobHunting/32772225_3.html)

> Given an int array A[], define: 

> distance = A[i] + A[j] + (j-i), j >= i. 

> Find max distance in A[]

### Solution

Solution suggested on floor 8 of [this post](http://www.mitbbs.com/mitbbs_article_t.php?board=JobHunting&gid=32772225&ftype=0). 

1. distance = (A[i] - i) + (A[j] + j), so we do 2 iteration in the array and calculate (A[i] - i) and (A[j] + j) respectively. 

1. save the max value of (A[i] - i) from left to right

1. save the max value of (A[j] + j) from right to left

1. last iteration, calculate result. 

Eg. input = {3, 3, 3, 5, 6, 4}

> max value of (A[i] - i) from left to right: {3, 3, 3, 3, 3, 3}
>
> max value of (A[j] + j) from right to left: {10, 10, 10, 10, 10, 9}
>
> final result: 13

### Code

__written by me__

	public int distance(int[] A) {
		int len = A.length;
		int[] arrayI = new int[len];
		int[] arrayJ = new int[len];

		arrayI[0] = A[0] - 0;
		// arrayI stores max value of (A[i]-i) from left to right
		arrayJ[len - 1] = A[len - 1] + (len - 1);
		// arrayJ stores max value of (A[i]+i) from right to left

		for (int i = 1; i < len; i++) {
			arrayI[i] = Math.max(arrayI[i - 1], A[i] - i);
		}

		for (int i = len - 2; i >= 0; i--) {
			arrayJ[i] = Math.max(arrayJ[i + 1], A[i] + i);
		}

		Common.printArray(arrayI);
		Common.printArray(arrayJ);

		int max = Integer.MIN_VALUE;
		for (int i = 0; i < len; i++) {
			max = Math.max(max, arrayI[i] + arrayJ[i]);
		}
		return max;
	}
