---
layout: post
title: "[Facebook] Hamming Distance of Array"
comments: true
category: q-facebook
tags: [ src ]
---

### Question 

[link](http://www.glassdoor.com/Interview/-a-first-write-a-function-to-calculate-the-hamming-distance-between-two-binary-numbers-b-write-a-function-that-takes-QTN_450885.htm)

> [Hamming distance](http://en.wikipedia.org/wiki/Hamming_distance) between two strings of equal length is the number of positions at which the corresponding symbols are different. 

> Write a function that takes a list of binary numbers and returns the sum of the hamming distances for each pair. 

> Do it in O(n) time. 

### Solution

The naive solution is O(n^2), so we simplify this question by using {0,0,0,1,1} as input. The output in this case would be 6. Why? Because 3 x 2 = 6. 

So the equation for solution would be: 

> distance (for a bit) = number of '1's * number of '0's

The final answer would be the sum of distances for all bits. The solution is from [this blog](http://se7so.blogspot.sg/2014/02/how-to-prepare-for-interview-9.html). 

### Code

Great solution, __not written by me__ 

	int hammingDist(int[] nums) {

		int[] bits = new int[32];

		for (int i = 0; i < nums.length; i++) {
			int one = 1;
			int j = 0;

			while (nums[i] != 0) {
				if ((nums[i] & one) != 0)
					bits[j]++;
				j++;
				nums[i] = nums[i] >> 1;
			}
		}

		int ans = 0;
		for (int i = 0; i < 32; i++) {
			ans += bits[i] * (nums.length - bits[i]);
		}

		return ans;
	}
