---
layout: post
title: "[Question] Print Numbers containing 5"
comments: true
category: Question
tags: [ src ]
---

### Question

[link](http://www.mitbbs.com/article_t/JobHunting/32651839.html)

> 写一个function，对于参数n，输出从0到n之间所有含5的数字。eg. func(30) 应该输出5，15，25

> this is Groupon interview question

### Solution

Suggested by level 10 of [this forum](http://www.mitbbs.com/article_t/JobHunting/32651839.html). __The key is to consider numbers as string, not numbers__. Why? The key of the question is to find "5" in a number. We do not really care about values. We care about characters instead! 

>用递归，基本思路是，
>
>考虑第i位的数字，取得值可以是0-9；唯一要注意的是最后一位数字，如果5没有出现过，只能取5.

In other words, iterate thru the numbers one by one. Discard numbers that are larger than n. Discard numbers that don't have "5". We are left will all the valid output. 

It's surprising to me that this is a __String + DFS__ question. 

### Code

__written by me__

	public void mySolution(int num) {
		if (num >= 5) {
			String str = String.valueOf(num);
			helper(num, "", 0, str.length(), false);
		}
	}

	private void helper(int max, String prefix, int pos, int len, boolean have5) {
		if (pos == len) {
			int cur = Integer.parseInt(prefix);
			if (cur <= max) {
				System.out.print(cur + ", ");
			}
			return;
		}
		for (int i = 0; i < 10; i++) {
			if (pos == len - 1 && !have5 && i != 5) {
				continue;
			}
			helper(max, prefix + i, pos + 1, len, have5 || i == 5);
		}
	}
