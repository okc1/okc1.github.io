---
layout: post
title: "[ItInt5] Numbers Concatenation Max (Largest Number) "
comments: true
category: Question
tags: [ ItInt5 ]
---

### Question

[link](http://www.itint5.com/oj/#45)

> 数组nums中有n个非负整数（整数用字符串表示），将它们以一定的顺序拼接，得到最大的整数。

> 样例：

> nums: ["54", "546", "548", "60"]

> 可以拼接得到的最大整数为"6054854654"，因此函数应该返回"6054854654"。

### Solution

__I will first list out 2 special cases__:

> {40, 20, 201} => 4020201
>
> {40, 20, 203} => 4020320

Knowing about this 2 cases helps us to come up with a sorting-based algorithm. We only need to achieve this:

> 201 < 20
>
> 20 < 203

So the best comparator implementation would be:

    String firstNum = s1 + s2;
    String secondNum = s2 + s1;
    return firstNum.compareTo(secondNum);

### Code

__written by me__.

	public String biggestNum(String[] nums) {
		Arrays.sort(nums, new SpecialComparator());
		StringBuilder sb = new StringBuilder();
		for (int i = nums.length - 1; i >= 0; i--) {
			sb.append(nums[i]);
		}
		return sb.toString();
	}

	class SpecialComparator implements Comparator<String> {
		public int compare(String s1, String s2) {
			// eg.
			// 40 > 20
			// 20 > 201
			// 203 > 20
			String firstNum = s1 + s2;
			String secondNum = s2 + s1;
			return firstNum.compareTo(secondNum);
		}
	}
