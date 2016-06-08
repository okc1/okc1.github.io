---
layout: post
title: "[LeetCode Plus] Coins in a Line "
comments: true
category: leetcode_plus
tags: [ unit test needed ]
---

### Question 

[link](http://leetcode.com/2011/02/coins-in-line.html)

> There are n coins in a line. Two players take turns to take a coin from one of the ends of the line until there are no more coins left. The player with the larger amount of money wins. Assume that you go first, describe an algorithm to compute the maximum amount of money you can win. 

> There might be even or odd number of coins. 

### Analysis

__There's a guaranteed 'win strategy'__, if the input array is even size. Find the sum of coins at even and odd positions respectively. Then, make sure you always take coin from even (or odd, whichever sum is bigger) position. 

This strategy is clever and simple, but __DOES NOT maximize your total sum__, and coins must be even number. 

### Solution

__The optimized solution is to use [2D DP](http://tech-queries.blogspot.sg/2011/06/get-maximum-sum-from-coins-in-line.html)__. Now we have array A and C(i, j) which is the maximum sum possible when remaining coins are from i to j. 

You can take either i or j. Since the opponent is as smart as you, he would have chosen the choice that yields the minimum amount to you. 

So, the final equation is: 

> C(i, j) = MAX {
>
>           Ai + MIN{C(i+2, j), C(i+1, j-1)}, 
>
>           Aj + MIN{C(i+1, j-1), C(i, j-2)} 
>
> }

If interested, read __[Fundamental] Min-Max Algorithm__ for more. 

### Code

	public int maxMoney(int[] coins) {
		int len = coins.length;
		int[][] dp = new int[len][len];
		for (int i = len - 1; i >= 0; i--) {
			for (int j = i; j < len; j++) {
				if (i == j) {
					dp[i][j] = coins[i];
				} else if (i + 1 == j) {
					dp[i][j] = Math.max(coins[i], coins[j]);
				} else {
					int chooseHead = coins[i]
							+ Math.min(dp[i + 2][j], dp[i + 1][j - 1]);
					int chooseTail = coins[j]
							+ Math.min(dp[i][j - 2], dp[i + 1][j - 1]);
					dp[i][j] = Math.max(chooseHead, chooseTail);
				}
			}
		}
		return dp[0][len - 1];
	}
