---
layout: post
title: "[Question] Greatest Common Divisor"
comments: true
category: Question
tags: [ src ]
---

### Question 

> Get GCD in more efficient code

### Code

this is 掉渣天。

	public int gcd(int a, int b) {
		return b == 0 ? a : gcd(b, a % b);
	}
