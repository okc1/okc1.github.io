---
layout: post
title: "[CC150v4] 19.4 Get Max Number without Comparator "
comments: true
category: CC150v4
tags: [ src ]
---

### Question

> Write a method which finds the maximum of two numbers. You should not use if-else or any other comparison operator.

> EXAMPLE
>
> Input: 5, 10
>
> Output: 10

This is also on __CC150v5 Q17.4__. 

### Solution

We can't use >, < or if-else statement, but we can use mathematical operator like subtract and bit operators. 

Calculate (a-b) and do (a + K(a-b)) can help us (where K is either 0 or -1). 

__Updated on Sep 29th__: according to CC150v5 Q17.4, there can be errros when __(a-b) is overflows__. So this is the modified version of solution: 

1. do a sign check of a and b
1. if a and b are same sign, do it just like before
1. if a and b are different sign, the 'K' value only depends on a. 

I posted the modified solution below as well. 

### Code

__first solution from v4__, written by me:

	public static int getMax(int a, int b) {
		int c = a - b;
		int signBit = c >> 31 & 1;
		// if (a-b) is negative, sign = 1
		// otherwise, sign = 0
		return a - signBit * c;
	}

__modified solution__, no overflow issues. 

	public static int getMax(int a, int b) {
		int sign;
		// if a,b have different sign, then go with first number
		if (sign(a) == sign(b)) {
			sign = sign(a - b);
		} else {
			sign = sign(a);
		}
		// sign is 0 if a >= b
		// sign is -1 is a < b
		return a + (a - b) * sign;
	}

	private static int sign(int c) {
		return c >> 31;
	}
