---
layout: post
title: "[Facebook] Scheduling Jobs with Max Cost "
comments: true
category: q-facebook
tags: [ src ]
---

### Question 

[link](http://www.glassdoor.com/Interview/Given-a-set-of-n-jobs-with-start-time-end-time-cost-find-a-subset-so-that-no-2-jobs-overlap-and-the-cost-is-maximum-QTN_440168.htm)

> Given a set of n jobs with [start time, end time, cost], find a subset so that no 2 jobs overlap and the cost is maximum.

> Let's assume the input is already sorted by start_time. 

### Solution

[Somebody](http://cs.stackexchange.com/a/14237) mentioned __Interval Graph__, so check it out if you interested! 

I am going to discuss both DP and recursive solution. 

This question reminds me of __[Question] 0-1 Knapsack Problem__ and __[Question] Coin Change Problem__, cuz the basic idea is to compare 2 conditions: 

1. include current element
1. or, not include current element

A very good DP solution is presented in [here](http://cs.stackexchange.com/a/16842). The code below is written by me and it's very intuitive to read. 

Leave me a comment if you have questions. And one more thing~ Happy new year! 

### Code

Dp

	private int dpSolution(Job[] jobs, int size) {
		int[] dp = new int[size];
		dp[size - 1] = jobs[size - 1].cost;
		// cost of last job equals to just itself
		for (int k = size - 2; k >= 0; k--) {
			int next = findNextJob(jobs, k);
			int includeK = jobs[k].cost;
			if (next < size) {
				includeK += dp[next];
			}
			int excludeK = dp[k + 1];
			dp[k] = Math.max(includeK, excludeK);
		}
		return dp[0];
	}

	private int findNextJob(Job[] jobs, int k) {
		int finishTime = jobs[k].finish;
		int next = k + 1;
		while (next < jobs.length) {
			if (jobs[next].start < finishTime) {
				next++;
			} else {
				break;
			}
		}
		return next;
	}

Recursion

	public int recursiveSolution(Job[] jobs, int size, int k) {
		// max cost from (k)th job and onwards
		if (k == size) {
			return 0;
		}
		// (k)th job must not conflict with any previous job
		int next = findNextJob(jobs, k);
		int includeK = jobs[k].cost + recursiveSolution(jobs, size, next);
		int excludeK = recursiveSolution(jobs, size, k + 1);
		return Math.max(includeK, excludeK);
	}

	private int findNextJob(Job[] jobs, int k) {
		int finishTime = jobs[k].finish;
		int next = k + 1;
		while (next < jobs.length) {
			if (jobs[next].start < finishTime) {
				next++;
			} else {
				break;
			}
		}
		return next;
	}
