---
layout: post
title: "[Java OOP] Octal and Hexadecimal Numbers in Java"
comments: true
category: Java OOP
tags: [ src ]
---

### Question 

[link](http://www.geeksforgeeks.org/g-fact-61/)

> Predict the output of following program.

	public static void main(String[] args) {
		int a = 012;
		System.out.println("a is " + a);
	}

### Analysis

Putting a 0 before an integer constant makes it an __octal number__ and putting 0x (or 0X) makes it a __hexadecimal number__.

__Answer: 10__.
