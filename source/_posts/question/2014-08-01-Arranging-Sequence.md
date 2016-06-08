---
layout: post
title: "[Question] Arranging Sequence "
comments: true
category: Question
tags: [ src ]
---

### Question 

[link](http://tech-queries.blogspot.sg/2008/11/arranging-sequence.html)

> We have an array of 2n elements like "a1 a2...an b1 b2...bn". WAP to rearrange the array as "a1 b1 a2 b2...an bn"

> time complexity is O(n) no extra array or memory can be taken.

> Input : 1 2 3 4 5 6 7 8 9 10 11 12 (even number input)
>
> Output: 1 7 2 8 3 9 4 10 5 11 6 12

> Input : 1 2 3 4 5 6 7 (odd number input)
>
> Output: 1 5 2 6 3 7 4

### Analysis

This is a difficult question. 

I did not find enough resources online, but have come up with 2 solutions.

### Solution

__First is like bubble sort (read it somewhere before)__. Always swap in pairs (starting from the middle): 

	1st: 1 2 3 4 5 6 7
	2nd: 1 2 3 5 4 6 7
	3rd: 1 2 5 3 6 4 7
	4th: 1 5 2 6 3 7 4
	done

__Second solution is to swap in cycles (put current value in its 'successor' position, and continue from there)__. But in order to identify cycles, additional space is used. I wrote the solution making use of 'visited' array. The time complexity is between O(n) and O(n^2). 

More info on this topic can be found on [wikipedia](http://en.wikipedia.org/wiki/In-place_matrix_transposition). 

### Code

__written by me__

	public void rearrange(int[] A) {
		int effLength = A.length;
		if (A.length % 2 == 0) {
			// for even number of input, last element is unchanged
			effLength--;
		}
		// make sure 'effLength' is an odd number.
		int half = effLength / 2 + 1;
		int pos = 1;
		int posValue = A[pos];
		int numSwaps = 0;
		boolean[] visited = new boolean[effLength];
		// visited is used as flag to avoid repeat swap
		// eg. when input is { 1, 2, 3, 4, 5, 6, 7 }, repeat swap as below:
		// 2 -> 3 -> 5 -> 2 -> 3 ...
		while (numSwaps < effLength - 1) {
			// swap (effLength - 1) times because 1st position is unchanged
			int newPos = getNewPosition(A, pos, half);
			if (visited[newPos]) {
				// if this new position is swap already, skip it
				pos = (pos + 1) % effLength;
				posValue = A[pos];
				continue;
			}
			int temp = A[newPos];
			A[newPos] = posValue;
			posValue = temp;
			pos = newPos;

			visited[newPos] = true;
			numSwaps++;
		}
	}

	private int getNewPosition(int[] array, int pos, int half) {
		if (pos < half) {
			return 2 * pos;
		} else {
			return 2 * (pos - half) + 1;
		}
	}
