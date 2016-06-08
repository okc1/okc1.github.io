---
layout: post
title: "[Question] All distinct subsequences with given length "
comments: true
category: Question
tags: [ src ]
---

### Question

[link](http://11011110.livejournal.com/254164.html)

> Find a polynomial-time algorithm that takes a string of length n, and a number k, output the number of distinct k-character subsequences.

> For instance, input "food" and number k=2, output should be 4. There are four distinct 2-character subsequences of "food": "fo", "fd", "oo", and "od".

### Solution

Similar to __[Question] Number of distinct sub-sequence__, we solve this problem with DP. The dp equation is a bit difficult to write. 

The idea come from comment from [gareth_rees](http://11011110.livejournal.com/254164.html): 

> Let θ(S, k) be the number of distinct k-character subsequences in the string S of length n. 

> Clearly θ(S, k) = 1 if n = k or k = 0 

> and θ(S, k) = 0 if n < k. 

> Otherwise, __choose 1 unique char from S__, and deduct k by 1, then do the DP calculation with the remaining part of S. 

Look at this example: 

    θ("food", 2) = θ("ood", 1) + θ("od", 1) + θ("", 1)
    = (θ("od", 0) + θ("", 0)) + (θ("d", 0) + θ("", 0)) + 0
    = (1 + 1) + (1 + 1)
    = 4

__"food" is divided into 3 parts__. First part we choose "f" to be the first char, thus the value is θ("ood", 1). Second part we choose "o", and final part we choose "d". 

__Note that when we choose a char, it must never have been chosen before__. In case of "food", we only choose 'f', 'o', 'd' once for each. 

This is a very difficult DP question, but the explanation really makes the answer easier. Read my implementation below. 

### Code

	public int countSubSeq(String input, int k) {
		// assuming all input chars are small letter
		return choose(input, 0, k);
	}

	private int choose(String input, int start, int numChar) {
		int charLeft = input.length() - start;
		if (charLeft == numChar || numChar == 0) {
			return 1;
		} else if (charLeft < numChar || numChar < 0) {
			return 0;
		}
		// now numChar is smaller than charLeft, and larger than 0
		// start to pick a char (which is at first appearance)
		int total = 0;
		HashSet<Character> chosen = new HashSet<Character>();
		while (start < input.length()) {
			char currentChar = input.charAt(start);
			if (!chosen.contains(currentChar)) {
				// pick the char pointer by 'start'
				total += choose(input, start + 1, numChar - 1);
				chosen.add(currentChar);
			}
			start++;
		}
		return total;
	}
