---
layout: post
title: "[CC150v4] 8.4 Generate Permutation Recursively "
comments: true
category: CC150v4

---

### Question

> Write a method to compute all permutations of a string. 

> Do it recursively. 

### Solution

1. Get first char. 

1. Permute the reminder of the string.

1. Insert that char into all possible positions. 

The code is more concise that doing it iteratively, __and no visited array needed__! 

### Code

	public static ArrayList<String> getPerms(String s) {
		ArrayList<String> ans = new ArrayList<String>();
		if (s.length() == 1) {
			ans.add(s);
			return ans;
		}
		char single = s.charAt(0);
		ArrayList<String> partialPerms = getPerms(s.substring(1));
		for (String part : partialPerms) {
			for (int i = 0; i <= part.length(); i++) {
				ans.add(part.substring(0, i) + single + part.substring(i));
			}
		}
		return ans;
	}
