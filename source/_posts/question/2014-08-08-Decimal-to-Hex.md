---
layout: post
title: "[Question] Decimal to Hexadecimal"
comments: true
category: Question
tags: [ src ]
---

### Question 

[link](http://stackoverflow.com/questions/13465098/decimal-to-hexadecimal-converter-in-java)

> Decimal to Hexadecimal conversion. 

### Solution

Convert binary to hex as a group of 4 bits. 

Read code. 

### Code

__written by me__

	private final char[] hexDigits = { '0', '1', '2', '3', '4', '5', '6', '7',
			'8', '9', 'A', 'B', 'C', 'D', 'E', 'F' };
	private final int flag = 0x0F;

	public String decToHex(int dec) {
		char[] hex = new char[8];
		for (int i = 7; i >= 0; i--) {
			int oneDigit = flag & dec;
			dec >>= 4;
			hex[i] = hexDigits[oneDigit];
		}
		return String.valueOf(hex);
	}
