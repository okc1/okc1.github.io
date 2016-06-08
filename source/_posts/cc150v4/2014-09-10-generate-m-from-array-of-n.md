---
layout: post
title: "[CC150v4] 20.3 Generate M int from Array of Size N "
comments: true
category: CC150v4
tags: [ src ]
---

### Question

> Write a method to randomly generate a set of m integers from an array of size n. Each element must have equal probability of being chosen. 

### Solution

This is very similar to another post I wrote: __[Question] Shuffle An Array (Fisher–Yates)__.

The basic idea is to choose element one by one using RNG. After choosing an int, swap it to top and __then mark this element as 'dead'__. Next time, the RNG will not touch on the 'dead' elements. 

__Very similar to Fisher–Yates Shuffle__, and the code below is written by me. 

### Code

	public static int[] pickMRandomly(int[] original, int m) {
		int[] ans = new int[m];
		for (int i = 0; i < m; i++) {
			int rand = Question.listRand.get(i);
			// note: rand is RN in the range [i, max]
			ans[i] = original[rand];
			original[rand] = original[i];
			// now (i)th position in original is dead
			// no one cares what value is at original[i]
		}
		return ans;
	}
