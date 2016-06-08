---
layout: post
title: "[LinkedIn] Unique combination of factors (因式分解) "
comments: true
category: Question

---

### Question 

[link](http://www.mitbbs.com/article_t1/JobHunting/32803907_0_1.html)

> A question by dongfeiwww: 

> 打印一个数的所有乘数组合，从大到小，不要有重复

> Print all unique combinations of factors of a positive integer. For example given 24:

    24*1
    12*2
    8*3
    6*4
    6*2*2
    4*3*2
    3*2*2*2

### Solution

Simple DFS.

### Code

	public List<List<Integer>> factorCombinations(int n) {
		List<List<Integer>> ans = new ArrayList<List<Integer>>();
		helper(ans, n, n / 2, new ArrayList<Integer>());
		return ans;
	}

	private void helper(List<List<Integer>> ans, int num, int largestFactor,
			List<Integer> path) {
		if (num == 1) {
			ans.add(new ArrayList<Integer>(path));
			return;
		}
		for (int i = largestFactor; i > 1; i--) {
			if (num % i == 0) {
				path.add(i);
				helper(ans, num / i, i, path);
				path.remove(path.size() - 1);
			}
		}
	}
