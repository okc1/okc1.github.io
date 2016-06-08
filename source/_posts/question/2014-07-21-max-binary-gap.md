---
layout: post
title: "[Question] Max Binary Gap"
comments: true
category: Question
tags: [ src ]
---

### Question 

[link](http://www.programcreek.com/2013/02/twitter-codility-problem-max-binary-gap/)

> Problem: Get maximum binary Gap.

> For example, 9's binary form is 1001, the gap is 2.

### Solution

This question is a good practise of binary operations. 

### Code

__writen by me__

	private int solution(int num) {
		int max = 0;
		int boundary = -1;
		for (int i = 0; i < 32; i++) {
			int t = num & 1;
			num = num >> 1;
			if (t == 1) {
				if (boundary == -1) {
					boundary = i;
				} else {
					max = Math.max(max, i - boundary - 1);
					boundary = i;
				}
			}
		}
		return max;
	}
