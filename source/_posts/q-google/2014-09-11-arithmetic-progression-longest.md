---
layout: post
title: "[Google] Length of Longest Arithmetic Progression (LLAP) "
comments: true
category: q-google
tags: [ src ]
---

### Question 

[link](http://www.careercup.com/question?id=8211177)

> Given an array of integers A, give an algorithm to find the longest Arithmetic progression in it, i.e find a sequence i1 < i2 < … < ik, such that 

> A[i1], A[i2], …, A[ik] forms an arithmetic progression, and k is the largest possible. 

> The sequence S1, S2, …, Sk is called an arithmetic progression if S(j+1) – S(j) is a constant. 

### Solution

__This is a rather difficult Arithmetic Progression question__. 

The solution is 2-D DP. 

> [The idea is](http://www.geeksforgeeks.org/length-of-the-longest-arithmatic-progression-in-a-sorted-array/) to create a 2D table dp[n][n]. An entry dp[i][j] in this table stores LLAP with input[i] and input[j] as first two elements of AP(j > i). 

> The last column of the table is always 2. Rest of the table is filled __from bottom right to top left__. 

> To fill rest of the table, j (second element in AP) is first fixed. i and k are searched for a fixed j. If i and k are found such that i, j, k form an AP, then __the value of dp[i][j] is set as dp[j][k] + 1__. 

> __Note that the value of dp[j][k] must have been filled__ before as the loop traverses from right to left columns. 

The 2 difficult points of this question:

1. how to come up with the transation formula. (i.e. __dp[i][j] = dp[j][k] + 1__, when (i, j, k) forms a AP). 
1. how to fill up all dp[i][j] in each loop of j. (Once inside the if-else, once outside the main while-loop) 

### Code

__written by me__

	public int longest(int[] A) {
		int len = A.length;
		int[][] dp = new int[len][len];
		for (int i = 0; i < len; i++) {
			// the pair ending at last position is always a progression
			dp[i][len - 1] = 2;
		}
		int longest = 1;
		for (int j = len - 2; j >= 0; j--) {
			// for each j, find i and k that makes 1 progression
			int i = j - 1;
			int k = j + 1;
			while (i >= 0 && k < len) {
				int total = A[i] + A[k];
				if (total > 2 * A[j]) {
					// this is important!
					dp[i][j] = 2;
					i--;
				} else if (total < 2 * A[j]) {
					k++;
				} else {
					// found a valid progression triplet A(i, j, k)
					dp[i][j] = dp[j][k] + 1;
					longest = Math.max(longest, dp[i][j]);
					i--;
					k++;
				}
			}
			// this is important!
			while (i >= 0) {
				dp[i][j] = 2;
				i--;
				// If the loop was stopped due to k becoming more than
				// n-1, set the remaining dp[i][j] as 2
			}
		}
		return longest;
	}
