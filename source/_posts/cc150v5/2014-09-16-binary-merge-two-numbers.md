---
layout: post
title: "[CC150v5] 5.1 Binary Merge 2 Numbers "
comments: true
category: CC150v5
tags: [ src ]
---

### Question

> You are given two 32-bit numbers, N andM, and two bit positions, i and j. Write a method to insert M into Nsuch that M starts at bit j and ends at bit i. You can assume that the bits j through i have enough space to fit all ofM. That is, ifM= 10011, you can assume that there are at least 5 bits between j and i. You would not, for example, have j-3 and i=2, because M could not fully fit between bit 3 and bit 2.

> EXAMPLE: 
>
> Input: N = 16000000000, M = 10011, i = 2, j = 6
>
> Output: N = 10001001100

### Solution

__This is a basic bit manipulation question__. The key is to use binary maks. Two things to note: 

1. The '~' means negate. So (~0) is a sequence of 1 (the value equals to -1). 

1. When shifting bits, __DO NOT USE '>>' because it's signed shift__. Instead, __use '>>>' (unsigned right shift operator)__. 

### Code

__written by me__

	public static int myAnswer(int n, int m, int i, int j) {
		int rr = (~0 >>> (31 - j));
		int ll = (~0 << i);
		// printBinary(rr);
		// printBinary(ll);

		int middleMask = ll & rr;
		int twoEndMask = ll ^ rr;

		n = n & twoEndMask;
		m = (m << i) & middleMask;

		return n | m;
	}
