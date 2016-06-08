---
layout: post
title: "[Question] Count Set Bit in Binary Number"
comments: true
category: Question
tags: [ src ]
---

### Question 

> Count Set Bit in Binary Number.

> 3 = 00000011 => 2

> 128 = 10000000 => 1

### Solution

__Bits counting algorithm__ (Brian Kernighan). Basic idea is __clear 1 bit at a time__. 

This algorithm goes through as many iterations as there are set bits. In the worst case, it will pass once per bit. An integer n has log(n) bits, hence [the worst case](http://stackoverflow.com/a/12381102) is O(log(n)).

### Code

	public int countSetBit(String binary) {
		int num = Integer.parseInt(binary, 2);
		int count = 0;
		while (num != 0) {
			num &= num - 1;
			count++;
		}
		return count;
	}
