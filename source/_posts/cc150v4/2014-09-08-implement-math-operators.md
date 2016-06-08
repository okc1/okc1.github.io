---
layout: post
title: "[CC150v4] 10.4 Implement Mathematical Operators"
comments: true
category: CC150v4

---

### Question

> Write a method to implement *, - , / operations You should use only the + operator. 

### Solution

__First it's important to write a 'negate' operator__. The code given in the book: 

	public static int FnNegate(int a) {
		int neg = 0;
		int d = a < 0 ? 1 : -1;
		while (a != 0) {
			neg += d;
			a += d;
		}
		return neg;
	}

__Updated on Feb 1st, 2015__, the negate method: 

	public static int negate(int a) {
		// plus -1, then do XOR with 111111111
		// eg. 1 -> 0000000 -> 11111111 = -1
		// eg. -1 -> 11111110 -> 00000001 = 1
		return (a + -1) ^ -1;
	}

And the check sign method: 

	public static boolean sameSign(int a, int b) {
		// if first bit is same, then xor = 00000000
		// if first bit is not same, xor = 10000000
		int xor = (a ^ b) & Integer.MIN_VALUE;
		return xor == 0;
	}

Although we can only use +, the author also used > and < comparison operators. 

### Code

	public static int negate(int a) {
		// plus -1, then do XOR with 111111111
		// eg. 1 -> 0000000 -> 11111111 = -1
		// eg. -1 -> 11111110 -> 00000001 = 1
		return (a + -1) ^ -1;
	}

	public static int minus(int a, int b) {
		return a + negate(b);
	}

	public static boolean sameSign(int a, int b) {
		// if first bit is same, then xor = 00000000
		// if first bit is not same, xor = 10000000
		int xor = (a ^ b) & Integer.MIN_VALUE;
		return xor == 0;
	}
