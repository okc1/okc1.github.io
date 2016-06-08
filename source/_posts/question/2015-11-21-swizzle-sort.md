---
layout: post
title: "[Question] Swizzle Sort "
comments: true
category: Question
tags: [  ]
---

# Question

[link](http://www.mitbbs.com/article_t/Recommend/31493121.html)

> 输入一个数组，要求输出满足：a[0]<=a[1]>=a[2]<=a[3]>=…

# Solution

> O(n)，一边扫描即可。发现不符合条件的只要跟前面一个数对调就可以，

# Code

	public int[] solve(int[] input) {
		boolean incr = true;
		int len = input.length;
		int p = 1;
		while (p < len) {
			if (incr ^ (input[p - 1] < input[p])) {
				Common.swap(input, p - 1, p);
			}
			p++;
			incr = !incr;
		}
		return input;
	}
