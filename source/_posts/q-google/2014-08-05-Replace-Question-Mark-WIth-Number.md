---
layout: post
title: "[Google] Replace Question Mark With Number"
comments: true
category: q-google
tags: [ src ]
---

### Question 

[link](http://www.careercup.com/question?id=5192571630387200)

> Given a string (for example: "a?bc?def?g"), write a program to generate all the possible strings by replacing ? with 0 and 1. 

> Input : a?b?c? 
>
> Output: a0b0c0, a0b0c1, a0b1c0, a0b1c1, a1b0c0, a1b0c1, a1b1c0, a1b1c1.

### Solution

DFS search, but do not forget to set "__letters[pos] = '?';__" at the end. I made this error once. 

### Code

	public List<String> solution(String str) {
		List<String> result = new ArrayList<String>();
		helper(result, str.toCharArray(), 0);
		return result;
	}

	private void helper(List<String> result, char[] letters, int pos) {
		if (pos == letters.length) {
			result.add(String.valueOf(letters));
			return;
		} else if (letters[pos] != '?') {
			helper(result, letters, pos + 1);
			return;
		}
		for (char i = '0'; i <= '1'; i++) {
			// put char i in letters[] to replace the '?'
			letters[pos] = i;
			helper(result, letters, pos + 1);
			letters[pos] = '?';
		}
	}
