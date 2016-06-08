---
layout: post
title: "[Google] Form a Palindrome with Insertion"
comments: true
category: q-google
tags: [ src ]
---

### Question 

[link](http://www.glassdoor.com/Interview/Given-a-string-convert-it-into-a-palindrome-with-the-lease-number-of-insertions-possible-QTN_729122.htm)

> Given a string, convert it into a palindrome with the lease number of insertions possible.

### Solution

This is a DP question. There're 2 approaches. 

__First, is direct DP__. This is the nicest solution, not intuitive at first, but actually good. 

> P[i, j] = P[i+1, j-1], if S[i] = S[j] 
>
> P[i, j] = 1 + min(P[i,j-1], P[i+1,j]), otherwise

contributed by [this guy](http://stackoverflow.com/a/10732879).

__Second approach is to calculate the longest palindrome subsequence__, and the answer would be string length minus this value. 

I wrote code for both apporaches. 

According to [G4G](http://www.geeksforgeeks.org/dynamic-programming-set-28-minimum-insertions-to-form-a-palindrome/), we can actually calculate the __Longest Common Subsequence of the string and its reverse__, and this value shall be same as the longest palindrome subsequence that we got in second approach. It's nice to know this idea.

### Code

__direct__

	public int solve1(String str) {
		// direct dp
		if (str == null)
			return 0;
		int len = str.length();
		int[][] dp = new int[len][len];
		for (int i = len - 1; i >= 0; i--) {
			for (int j = i; j < len; j++) {
				if (i == j) {
					dp[i][j] = 0;
				} else if (i + 1 == j) {
					dp[i][j] = str.charAt(i) == str.charAt(j) ? 0 : 1;
				} else {
					dp[i][j] = str.charAt(i) == str.charAt(j) ? dp[i + 1][j - 1]
							: 1 + Math.min(dp[i + 1][j], dp[i][j - 1]);
				}
			}
		}
		return dp[0][len - 1];
	}

__longest palindrome subsequence__

	public int solve2(String str) {
		// longest palindrome subsequence
		if (str == null)
			return 0;
		int len = str.length();
		int[][] dp = new int[len][len];
		for (int i = len - 1; i >= 0; i--) {
			for (int j = i; j < len; j++) {
				if (i == j) {
					dp[i][j] = 1;
				} else if (i + 1 == j) {
					dp[i][j] = str.charAt(i) == str.charAt(j) ? 2 : 1;
				} else {
					dp[i][j] = str.charAt(i) == str.charAt(j) ? 2 + dp[i + 1][j - 1]
							: Math.max(dp[i + 1][j], dp[i][j - 1]);
				}
			}
		}
		return len - dp[0][len - 1];
	}
