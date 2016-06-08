---
layout: post
title: "[CC150v4] 20.4 Count 2s in Digits "
comments: true
category: CC150v4
tags: [ src ]
---

### Question

> Write a method to count the number of 2s between 0 and n.

### Solution

__This is a difficult question__, especially hard to come up with the correct formula. Eg. 

> f(279) = {(79 + 1) + 2 * f(99)} + f(79)
>
> f(513) = {100 + 5 * f(99)} + f(13)

Take 513 as example, the first digit is 5. We know that all the 200+ is within the range, so __there're 100 twos in the first digit__. Then, for the rest of the digits, we get f(99) for number between 0 and 99, and another f(99) for number between 100 and 199... and __this happens 5 times until 499__. That's why we have 5 multiple by f(99). 

In the end, we do the calculation __recursively for reminder number 13__. 

### Code

	public static int myAnswer(int n) {
		if (n == 0)
			return 0;
		int power = 1;
		while (power * 10 <= n) {
			power *= 10;
		}

		int first = n / power;
		int reminder = n % power;
		int firstDigit2count = 0;
		if (first > 2) {
			firstDigit2count = power;
		} else if (first == 2) {
			firstDigit2count = reminder + 1;
		}
		int totalCountBeforeReminder = firstDigit2count
				+ (first * myAnswer(power - 1));
		return totalCountBeforeReminder + myAnswer(reminder);
	}