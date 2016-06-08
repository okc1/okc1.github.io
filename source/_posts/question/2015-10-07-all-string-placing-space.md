---
layout: post
title: "[Amazon] All Strings by Placing Spaces "
comments: true
category: Question
tags: [  ]
---

### Question

[link](www.geeksforgeeks.org/print-possible-strings-can-made-placing-spaces/index.html)

> Given a string, print all possible strings that can be made by placing spaces (zero or one) in between them.

> Input:  str[] = "ABC"

>Output:

        ABC
        AB C
        A BC
        A B C

### Solution

recursion.

### Code 


	public void printAll(String input) {
		if (input == null || input.length() <= 1) {
			// since we insert space in-between chars, so
			return;
		}
		int len = input.length();
		// len >= 2
		helper(input, len - 1);
	}

	private void helper(String s, int p) {
		if (p == 1) {
			System.out.println(s);
			// no insertion
			System.out.println(s.substring(0, 1) + " " + s.substring(1));
			// insert at position 1
		} else {
			helper(s, p - 1);
			helper(s.substring(0, p) + " " + s.substring(p), p - 1);
		}
	}
