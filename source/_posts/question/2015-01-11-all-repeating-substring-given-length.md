---
layout: post
title: "[LinkedIn] Find all repeating substring with given length "
comments: true
categories:
- Question
- z-string-search
tags: [ src ]
---

### Question

[link](http://www.careercup.com/question?id=6495932900179968)

> Find all the repeating substring of specified length in a large string sequence.

> For e.g. 

    Input String: "ABCACBABC" 
    repeated sub-string length: 3 
    Output: ABC 

> eg. 

    Input String: "ABCABCA" 
    repeated sub-string length: 2 
    Output: AB, BC, CA

### Solution

Similar to __[Amazon] Longest Repeating Substring__, the best solution is to do __Suffix Tree__, or suffix array. We then need to print nodes on a certain level, who has more than 1 descendant. 

However, since the length of substring is given, we can also do simply iteration: insert all substring with given length into a HashSet, and check repetition. [ref](https://github.com/techpanja/interviewproblems/blob/master/src/strings/repeatingstringsofspecifiedlength/RepeatingStringOfSpecificLength.java)

### Code

Suffix tree solution: not written. 

Hashset code:

	public List<String> solve(String input, int k) {
		List<String> ans = new ArrayList<String>();
		HashSet<String> set = new HashSet<String>();
		for (int i = 0; i <= input.length() - k; i++) {
			String sub = input.substring(i, i + k);
			if (set.contains(sub)) {
				ans.add(sub);
			}
			set.add(sub);
		}
		return ans;
	}
