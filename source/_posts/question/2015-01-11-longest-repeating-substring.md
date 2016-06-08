---
layout: post
title: "[Amazon] Longest Repeating Substring "
comments: true
categories:
- Question
- z-string-search
tags: [ src ]
---

### Question

[link](http://www.careercup.com/question?id=9182781)

> Finding the longest repeated substring. 

> Example: "banana" ==> "ana"

### Solution

There are 2 solutions: Suffix array, and Suffix tree. 

__1. Suffix array__. Simple code, explained [here](http://www.careercup.com/question?id=9182781).

> Bentley's programming pearl book has the simplest implementation (less than 15 lines code) which sort all suffix, and then check common prefix length among adjacent suffix. The time complexity is O(n^2logn) for sorting the suffix (which has avg length of O(n)). 

A detailed step-by-step [explanation](http://nriverwang.blogspot.com/2013/04/longest-repeated-substring.html): 

    str = banana, its suffixes are:
    banana
    anana
    nana
    ana
    na
    a

after sort, the suffix array looks like:

    a
    ana
    anana
    banana
    na
    nana

Then for each two adjacent suffixes, check the length of the common prefix.

The answer is "ana" (if overlapping is allowed, otherwise, should be "an"). 

__2. Suffix tree__. Suggest by [this post](http://qr.ae/6W9yJ), Or [this](http://www.careercup.com/question?id=9182781):

> a good solution is to create a suffix tree for the given word and then find the deepest internal node in that tree (node with at least 2 descendants under it)...

For a nice PPT presentation about suffix tree, look [here](https://www.cs.cmu.edu/~ckingsf/bioinfo-lectures/suffixtrees.pdf). 

### Code

Suffix array approach. 

	public String longestRepeat(String input) {
		int len = input.length();
		String[] suffixArray = new String[len];
		for (int i = 0; i < len; i++) {
			suffixArray[i] = input.substring(i);
		}
		// now sort the suffix array
		Arrays.sort(suffixArray);
		String longest = "";
		// start to compare neighborhood suffixes, and check LCP
		for (int i = 0; i < suffixArray.length - 1; i++) {
			String lcp = longestCommonPrefix(suffixArray[i], suffixArray[i + 1]);
			if (lcp.length() > longest.length()) {
				longest = lcp;
			}
		}
		return longest;
	}

	private String longestCommonPrefix(String s1, String s2) {
		int p = 0;
		while (p < s1.length() && p < s2.length()) {
			if (s1.charAt(p) != s2.charAt(p)) {
				break;
			}
			p++;
		}
		return s1.substring(0, p);
	}
