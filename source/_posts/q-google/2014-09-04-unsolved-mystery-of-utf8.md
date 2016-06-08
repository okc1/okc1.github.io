---
layout: post
title: "[Google] Unsolved Mystery of UTF8 Encoding"
comments: true
category: q-google

---

### Question 

[link](http://algorithmguru.com/blog/?p=148)

> UTF-8 is a variable-length encoding of letters or runes. If the most significant bit of the first byte is 0, the letter is 1 byte long. Otherwise, its length is the number of leading 1’s in the first byte. If a letter is more than one byte long, all subsequent runes start with 10. Here’s a chart:

> UTF-8 encoding scheme is described below:

	0XXXXXXX = this is the entire rune
	10XXXXXX = this is a continuation of the rune from the previous byte
	110XXXXX = this is the start of a 2-byte rune.
	1110XXXX = this is the start of a 3-byte rune.
	11110XXX = this is the start of a 4-byte rune.
	111110XX = this is the start of a 5-byte rune.
	1111110X = this is the start of a 6-byte rune.
	11111110 = this is the start of a 7-byte rune.
	11111111 = this is the start of a 8-byte rune.

> For example, a 3-byte rune would be 1110XXXX 10XXXXXX 10XXXXXX.

> Write a function that decides whether a given byte array (or string) is valid UTF-8 encoded text. 

### Solution

This is an easy question, just put here for reference. 
