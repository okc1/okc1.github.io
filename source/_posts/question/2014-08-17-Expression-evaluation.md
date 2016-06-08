---
layout: post
title: "[Twitter] Arithmetic Expression Evaluation"
comments: true
category: Question

---

### Question 

[link](http://www.itint5.com/oj/#26)

> 给定一个表达式字符串，其中只包含非负整数，加法，减法以及乘法符号，例如7+3*4*5+2+4-3-1。请写程序计算该表达式的值。

> 提示：可以尝试使用递归算法，程序将非常简洁易写，很适用于面试场合。

### Solution

__Trying to solve this problem iteratively is like suicide__. The code would be lengthy and buggy, and very hard to make it right. 

__The most important point about this question, is how to handle minus(-) sign__. We know that when we see * and /, we evaluate immediately, and when sees + and -, we postpone it. However this case: 

> 1 - 2 - 3

If we postpone the first minus sign, we would end up getting: 

> 1 - (-1)

So it's wrong (outputing 2 in this case). 

__The solution to this issue is, consider (a - b) as (a + (-b))__. That's why later in the code, you'll see a variable __preNum__ being modified. 

[ref](http://www.itint5.com/discuss/50/case%E9%87%8C%E9%9D%A2%E6%9C%89%E4%B8%80%E4%B8%AA%E5%B8%A6%E8%B4%9F%E6%95%B4%E6%95%B0%E7%9A%84%EF%BC%8C%E5%B9%B6%E6%B1%82%E9%80%92%E5%BD%92%E5%AE%9E%E7%8E%B0)

### Code

__written by me__

	int p;

	public int evaluate(String expr) {
		p = 0;
		int firstNum = getNumber(expr);
		return helper(firstNum, expr);
	}

	private int helper(int preNum, String expr) {
		// now p points to a operator (or end of string)
		if (p == expr.length()) {
			return preNum;
		}
		char operator = expr.charAt(p);
		p++;
		int nextNum = getNumber(expr);
		switch (operator) {
		case '+':
			return preNum + helper(nextNum, expr);
		case '-':
			return preNum + helper(-1 * nextNum, expr);
		case '*':
			return helper(preNum * nextNum, expr);
		default:
			return helper(preNum / nextNum, expr);
		}
	}

	private int getNumber(String expr) {
		// now p points to a number
		int num = 0;
		while (p < expr.length() && expr.charAt(p) >= '0'
				&& expr.charAt(p) <= '9') {
			num = num * 10 + expr.charAt(p) - '0';
			p++;
		}
		return num;
	}
