---
layout: post
title: "[Question] 0-1 Knapsack Problem"
comments: true
category: Question

---

### Question 

[link](http://www.geeksforgeeks.org/dynamic-programming-set-10-0-1-knapsack-problem/)

> Given weights and values of n items, put these items in a knapsack of capacity W to get the maximum total value. 

> In other words, given two integer arrays val[0..n-1] and wt[0..n-1] which represent values and weights. Also given an integer W which represents knapsack capacity, find out the maximum possible value. 

> You cannot break an item, either pick it or don’t pick it (0-1 property). 

### Analysis

This is a very similar question to __[Question] Coin Change Problem__, because directly using recursion to solve will result in a lot of re-calculations. It's a DP question. 

### Solution

First of all, define a 2D array, Knapsack(n,W) denotes getting 'n'th item, with weight 'W'. When n == 0 or W = 0, dp value is 0. 

> int[][] Knapsack = new int[n + 1][W + 1];

Using 'n' to denote the items to put into Knapsack. 'v' is the value and 'w' is the total weight. 

Now if item 'n' is able to fit in:

> Knapsack(n,W) = max(vn + Knapsack(n-1, W-wn), Knapsack(n-1, W))

If not able to fit in: 

> Knapsack(n,W) = Knapsack(n-1, W)

Refer to page 11 to 12 of [this pdf](http://www.cs.rit.edu/~zjb/courses/800/lec7.pdf).

### Follow up

Look at the code, we checked dp[i-1][j]. Now the question is: 

> Do we need to check dp[i][j-1] ? (In case that total weight is not fully used up)

The answer is NO. We don't. Look at example: weights = {1, 2} and values = {3, 5}, and knapsack weight = 4. DP array would be: 

    [
     [0, 0, 0, 0, 0],
     [0, 3, 3, 3, 3],
     [0, 3, 5, 8, 8]
    ]

See that? The way that we keep DP array size int[items + 1][totalWeight + 1], the DP value is always 0 at 1st column and row. 

So, in the example when i == 1, total value is ALWAYS 3. 

### Code

	public int maxValNoDup(int totalWeight, int[] value, int[] weight) {
		int items = value.length;
		Arrays.sort(value);
		Arrays.sort(weight);

		int[][] dp = new int[items + 1][totalWeight + 1];
		for (int i = 1; i <= items; i++) {
			for (int j = 1; j <= totalWeight; j++) {
				// we'll try to take i'th item, to fit in weight j
				if (j < weight[i - 1]) {
					// not able to put in
					dp[i][j] = dp[i - 1][j];
				} else {
					// we are able to take i'th item into knapsack
					dp[i][j] = Math.max(dp[i - 1][j], value[i - 1]
							+ dp[i - 1][j - weight[i - 1]]);
				}
			}
		}
		return dp[items][totalWeight];
	}
