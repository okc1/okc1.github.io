---
layout: post
title: "[Amazon] Lexicographic rank of a string "
comments: true
category: Question
tags: [ src ]
---

### Question

[link](http://www.geeksforgeeks.org/lexicographic-rank-of-a-string/)

> Given a string, find its rank among all its permutations sorted lexicographically. 

> For example, rank of “abc” is 1, rank of “acb” is 2, and rank of “cba” is 6.

### Solution

Let the given string be “__STRG__”. In the input string, ‘S’ is the first character. There are total 4 characters and __2 of them are smaller than ‘S’__. So there can be __2 * 3!__ smaller strings where first character is smaller than ‘S’, like following: 

    G X X X
    R X X X

Repeat the same process for T, and we get: 

    Rank = 2*3! + 2*2! + 1*1! + 0*0! = 17

### Code 

	public int getRank(String input) {
		if (input == null || input.length() == 0) {
			return 0;
		}
		input = input.toUpperCase();
		return helper(input) + 1;
	}

	public int helper(String input) {
		if (input == null || input.length() == 0) {
			return 0;
		}
		char headChar = input.charAt(0);
		int countSmallerThanHead = 0;
		for (char ch : input.toCharArray()) {
			if (ch < headChar) {
				countSmallerThanHead++;
			}
		}
		return countSmallerThanHead * Common.factorial(input.length() - 1)
				+ helper(input.substring(1));
	}
