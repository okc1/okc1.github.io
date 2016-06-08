---
layout: post
title: "[Question] Frog Crossing (dynamic programming) "
comments: true
category: Question

---

### Question 

[link](https://tkramesh.wordpress.com/2011/02/15/frog-crossing-more-on-dynamic-programming-3/)

> A frog wants to cross the river n meters wide. There're some stones, but not complete from 1 to n. 

> The frog has a peculiar jumping rule. If it jumps x meters on one jump, the next jump has to lie in the range {x-1, x, x+1}. Further, the 1st jump that the frog makes is of exactly 1 meter.

> Given whether stones are removed or not as array of 0 and 1, check if it is possible to reach the other end.

### Solution

__This is a difficult DP question__. It can be solved in O(n^2) time. 

The main equation is: 

> can_reach [s, d] =
>
> Stone[d] AND Stone[s] AND [ can_reach [(d-s)-1, s] OR can_reach[d-s, s] OR can_reach[d-s)+1, s] ].
>
> where 's' is starting point, and 'd' is destination. 

### Code

	public boolean canCross(int[] stones) {
		if (stones.length < 2 || (stones[0] != 1 || stones[1] != 1)) {
			// invalid input data
			return false;
		}
		int n = stones.length;
		boolean[][] dp = new boolean[n][n];
		// dp[i][j] denotes that frog can jump from index i to j

		for (int i = 0; i < n; i++) {
			for (int j = i + 1; j < n; j++) {
				if (stones[i] == 0 || stones[j] == 0) {
					// if either stones i or stone j is removed, skip
					continue;
				}
				// note that j start from (i+1) because we make sure dp[i][i]
				// false. Otherwise, dp[i][i+1] will always be true

				if (i == 0) {
					// if jump from position 0, can only reach 1
					dp[i][j] = j == 1;
				} else {
					// if jump from other positions, need to check previous
					// distance, within range or not.
					int dis = j - i;
					for (int pre = i - dis - 1; pre <= i - dis + 1; pre++) {
						// pre is the previous position where frog jumps to i
						if (pre < 0) {
							continue;
						} else if (dp[pre][i]) {
							// frog jumps from pre to i, then frog is able to
							// jump from i to j
							dp[i][j] = true;
							break;
						}
					}
				}
				// finish calculating dp[i][j], now check termination
				if (j == n - 1 && dp[i][j]) {
					return true;
				}
			}
		}
		return false;
	}
