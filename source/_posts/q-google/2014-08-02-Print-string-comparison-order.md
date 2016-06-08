---
layout: post
title: "[Google] Print string comparison order"
comments: true
category: q-google
tags: [ src ]
---

### Question 

[link](http://www.careercup.com/question?id=5680043955060736)

> Output top N positive integer in string comparison order. For example, let's say N=1000, then you need to output in string comparison order as below: 

> 1, 10, 100, 1000, 101, 102, ... 109, 11, 110, ... 998, 999. 

### Solution

Thought for a while, and realize it's stanard DFS. 

### Code

__written by me__

	public static void main(String args[]) {
		for (int i = 1; i < 10; i++) {
			dfs("" + i);
		}
	}

	public static void dfs(String path) {
		if (Integer.parseInt(path) > 1000) {
			return;
		}
		System.out.println(path);
		for (int i = 0; i < 10; i++) {
			dfs(path + i);
		}
	}
