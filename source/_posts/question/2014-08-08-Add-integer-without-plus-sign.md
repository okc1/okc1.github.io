---
layout: post
title: "[Question] Add Integers without +/++"
comments: true
category: Question
tags: [ src ]
---

### Question 

[link](http://javarevisited.blogspot.sg/2013/06/how-to-add-two-integer-numbers-without-plus-arithmetic-operator-java-example.html)

> Add two numbers (integers) without using + or plus arithmetic operator.

### Solution

__Bit operations__. 

We could not do this in 1 pass, because multiple rounding issues. 

So we do it in while-loop then! 2 solutions available: __iteratively and recursively__. 

### Code

__written by me__

	public int add(int x, int y) {
		// add y into x (and y results to 0)
		while (y != 0) {
			int carry = x & y;
			int sum = x ^ y;
			x = sum;
			y = carry << 1;
		}
		return x;
	}

__recursive__

	public int add2(int x, int y) {
		if (y == 0) {
			return x;
		}
		int carry = (x & y) << 1;
		return add2(x ^ y, carry);
	}

__updated on Sep 10th, 2014__: this question appears on cc150v4 20.1. I wrote the following code: 

	public static int add_no_arithm(int a, int b) {
		if (b == 0)
			return a;
		int addition = a ^ b;
		int carry = (a & b) << 1;
		return add_no_arithm(addition, carry);
	}
