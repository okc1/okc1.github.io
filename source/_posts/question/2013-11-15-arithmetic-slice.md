---
layout: post
title: "[Question] Count Arithmetic Slices "
comments: true
category: Question
tags: [  ]
---

# Question

> Given an unsorted array of length N, a slice is defined as a pair of numbers (P, Q) so that:

> 1. 0 <= P < Q <= N
> 2. A[P], A[P+1]....A[Q] is arithmetic sequence

> Example: 

>     input = { -1, 1, 3, 3, 3, 2, 1, 0 }

> Output 5 because there're slices: 

>     (0, 2) (2, 4) (4, 6) (4, 7) (5, 7)

# Solution

1. count the length of arithmetic (countinuous) sequence
2. form some slices
3. proceed from the end of that sequence, till the end.

# Code

	public int solve(int[] input) {
		int len = input.length;
		int p = 0;
		int totalSlices = 0;

		while (p + 1 < len) {
			// check if there is a arithmetic sequence starting at p
			// note that p is NOT the last element.
			int diff = input[p + 1] - input[p];
			int q = p + 1;

			// starting from q, check arithmetic difference
			while (q < len) {
				if (input[q] - input[q - 1] == diff) {
					q++;
				} else {
					break;
				}
			}

			// so, the range [p, q-1] is a arithmetic sequence.
			int seqLength = q - p;
			if (seqLength >= 3) {
				totalSlices += getSlicesCountFromArithmeticSeq(seqLength);
			}

			// update p (skip the range [p, q-1])
			p = q - 1;
		}
		return totalSlices;
	}

	private int getSlicesCountFromArithmeticSeq(int k) {
		// choose 2 from (k - 1)
		return (k - 1) * (k - 2) / 2;
	}
