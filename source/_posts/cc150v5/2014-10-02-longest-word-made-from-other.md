---
layout: post
title: "[CC150v5] 18.7 Longest Word Made From Other Words "
comments: true
category: CC150v5
tags: [ src ]
---

### Question

> Given a list of words, write a program to find the longest word made of other words in the list.

> EXAMPLE
>
> Input: cat, banana, dog, nana, walk, walker, dogwalker
>
> Output: dogwalker

### Solution

__Search it recursively from longest to shortest__. Use HashSet to help us search for words quickly. 

This question might look difficult at first, it's actually a very classical recursive search. 

### Code

	public static void printLongestWord(String[] arr) {
		Arrays.sort(arr, new LengthComparator());
		HashSet<String> set = new HashSet<String>();
		for (String str : arr) {
			set.add(str);
		}
		for (String word : arr) {
			if (canDivide(word, 0, set)) {
				System.out.println(word);
				return;
			}
		}
		System.out.println("can not find such word");
	}

	private static boolean canDivide(String word, int from, HashSet<String> set) {
		if (from == word.length()) {
			return true;
		}
		for (int i = from; i < word.length(); i++) {
			String str = word.substring(from, i + 1);
			if (from == 0 && i == word.length() - 1) {
				continue;
			} else if (!set.contains(str)) {
				continue;
			}
			if (canDivide(word, i + 1, set)) {
				return true;
			}
		}
		return false;
	}
