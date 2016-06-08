---
layout: post
title: "[CC150v4] 9.5 Search Array Containing Empty String "
comments: true
category: CC150v4

---

### Question

> Given a sorted array of strings which is interspersed with empty strings, write a method to find the location of a given string. 

> Example: find “ball” in [“at”, “”, “”, “”, “ball”, “”, “”, “car”, “”, “”, “dad”, “”, “”] will return 4

> Example: find “ballcar” in [“at”, “”, “”, “”, “”, “ball”, “car”, “”, “”, “dad”, “”, “”] will return -1 

### Solution

The solution is binary search, but when reads empty, __advance to the next non-empty string__. 

But wait, __there can be a very big problem that causes looping forever__. Eg. 

> "a", "", "", "", "c" (5 items), look for "b"

> Now 'left' points to 1st string("a") and 'right' points to 4th(""). If we read read 'mid' value and advance to the next non-empty string, it'll be "c". 

> since "c" is large than "b", 'right' is set to the 4th index. It's a endless loop!

There're various ways to solve this. The book suggests __locate 'right' pointer at non-empty string__ by moving left, and then __locate 'mid' pointer at non-empty__ by moving right. This avoids endless loop. 

My approach is to use 2 instances of 'mid': 

1. calculatedMid
1. comparisonMid

Both ways are fine.

### Code

	public static int search(String[] input, String target) {
		if (target == null || target.length() == 0) {
			return -1;
		}
		int len = input.length;
		int left = 0, right = len - 1;
		while (left < right) {
			int calculatedMid = left + (right - left) / 2;
			int comparisonMid = calculatedMid;
			while (comparisonMid < len && input[comparisonMid].length() == 0) {
				comparisonMid++;
			}
			if (input[comparisonMid].equals(target)) {
				return comparisonMid;
			} else if (input[comparisonMid].compareTo(target) < 0) {
				left = comparisonMid + 1;
			} else {
				right = calculatedMid - 1;
			}
		}
		if (left < len && input[left].equals(target)) {
			return left;
		} else {
			return -1;
		}
	}
