---
layout: post
title: "[CC150v5] 17.14 Optimal Way to Unconcatenate Doc "
comments: true
category: CC150v5
tags: [ src ]
---

### Question

> Given a lengthy document without spaces, punctuation, and capitalization:

> eg: iresetthecomputeritstilldidntboot

> Now add back in the punctation and capitalization. 

> Most of the words will be in a dictionary, but some strings, like proper names, will not. Given a dictionary (a list of words), design an algorithm to find the optimal way of "unconcatenating" a sequence of words (by minimizing unrecognized sequences of characters).

> For example, the string "jesslookedjustliketimherbrother" would be optimally parsed as "JESS looked just like TIM her brother". This parsing has seven unrecognized characters, which we have capitalized for clarity. 

### Solution

The solution given in the book is very hard to understand. It uses HashMap to memorize the previous result. 

After long time of struggle, I finally solved it with traditional DP approach. The key idea is to consider: "__whether I insert a space after this char, or not__". 

The code is concise and easy to read. 

### Code

	public static int parse(String doc, Trie dict) {
		int len = doc.length();
		int[] dp = new int[len + 1];
		// dp[i] denotes the number of special chars in first i chars of docs
		for (int i = 1; i <= len; i++) {
			dp[i] =  Integer.MAX_VALUE;
			for (int j = 0; j < i; j++) {
				String str = doc.substring(j, i);
				if (dict.contains(str, true)) {
					// consider (i to j) a valid word
					dp[i] = Math.min(dp[i], dp[j]);
				} else {
					// consider (i to j) special chars
					dp[i] = Math.min(dp[i], dp[j] + i - j);
				}
			}
		}
		return dp[len];
	}
