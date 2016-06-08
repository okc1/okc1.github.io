---
layout: post
title: "[Google] Product All 1s"
comments: true
category: q-google
tags: [ src ]
---

### Question 

[link](http://www.itint5.com/oj/#18)

> 给定一个非负整数a（不超过10^6），是否存在整数b，使得a和b的乘积全为1。如果存在，返回最小的乘积的位数。如果不存在，返回-1。

> 样例：a=3，存在b=37，使得3*37=111，则函数应返回3（111的位数）。

### Solution

There's 1 equation of mod operation, which is helpful: 

> (a * b) mod x = ((mx+a') * (nx+b')) mod x = (a' mod x) * (b' mod x) = (a mod x) * (b mod x)
>
> i.e.  (a * b) mod x = (a mod x) * (b mod x)

Altough [I don't understand why](http://www.itint5.com/discuss/136/%E8%BF%99%E9%A2%98%E6%88%91%E8%B6%85%E6%97%B6%E4%BA%86%EF%BC%8C%E8%AF%B7%E9%97%AE%E5%A6%82%E4%BD%95%E7%BC%A9%E7%9F%AD%E5%A4%84%E7%90%86%E6%97%B6%E9%97%B4) does it contribute to the incredibly short solution code posted below. I can't solve this question, frankly speaking. 

### Code

	int findMinAllOne(int a) {
		if (a < 0 || (a % 10) % 2 == 0 || a % 10 == 5)
			return -1;

		int ans = 1;
		for (int p = 1; p != 0; p %= a) {
			p = 10 * p + 1;
			++ans;
		}
		return a == 1 ? ans - 1 : ans;
	}
