---
layout: post
title: "[CC150v4] 19.6 Convert Integer to English "
comments: true
category: CC150v4
tags: [ src ]
---

### Question

> Given an integer between 0 and 999,999, print an English phrase that describes the integer (eg, “One Thousand, Two Hundred Thirty Four”). 

This is also on __CC150v5 Q17.7__. 

### Solution

The solution in book isn't good, so I wrote the code myself. Read it below. 

### Code

	private static String[] arr1 = { "Zero ", "One ", "Two ", "Three ",
			"Four ", "Five ", "Six ", "Seven ", "Eight ", "Nine " };

	private static String[] arr11 = { "Ten ", "Eleven ", "Twelve ",
			"Thirteen ", "Fourteen ", "Fifteen ", "Sixteen ", "Seventeen ",
			"Eighteen ", "Nineteen " };

	private static String[] arr10 = { "", "Ten ", "Twenty ", "Thirty ",
			"Forty ", "Fifty ", "Sixty ", "Seventy ", "Eighty ", "Ninety " };

	public static String numtostring(int num) {
		int part1 = num / 1000;
		int part2 = num % 1000;
		if (part1 == 0) {
			return numBelowTrousand(part2);
		} else {
			return numBelowTrousand(part1) + "Thousand, "
					+ numBelowTrousand(part2);
		}
	}

	public static String numBelowTrousand(int num) {
		StringBuilder sb = new StringBuilder();
		// assume num is below 1000

		// first, convert hundred digit
		int hundred = num / 100;
		if (hundred != 0) {
			sb.append(arr1[hundred] + "Hundred ");
		}

		// second, convert the rest of digits
		num %= 100;
		if (num != 0) {
			int ten = num / 10;
			int one = num % 10;
			if (ten == 1) {
				sb.append(arr11[num - 10]);
			} else {
				if (ten != 0) {
					// ten is in the range of [2,9]
					sb.append(arr10[ten]);
				}
				if (one != 0) {
					sb.append(arr1[one]);
				}
			}
		}
		return sb.toString();
	}
