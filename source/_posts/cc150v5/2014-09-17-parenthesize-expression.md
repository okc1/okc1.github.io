---
layout: post
title: "[CC150v5] 9.11 Parenthesize the Expression "
comments: true
category: CC150v5
tags: [ src ]
---

### Question

> Given a boolean expression consisting of the symbols 0, 1, '&', '|', and '^', and a desired boolean result value 'result'. 

> Now implement a function to count the number of ways of __parenthesizing the expression__ such that it evaluates to 'result'.

### Solution

__This is a difficult question__.

> Each parenthesized expression must have an outermost pair of
parentheses. 

> That is, we can iterate through the expression, treating each operator as the first operator to be parenthesized. 

Nice idea suggested in the book! So __for each operator, we consider is as first operator (to evaluate)__, and then we shall if the total possible count. 

(Note that while coding, we DO NOT WRITE {if-else if-else...} but instead use {if... if... if...} in order to get the total count. )

DP is more time-efficient. 

__Like CC150v5 Q9.10, the code given in the book is very hard to read__. I have my own code posted below. 

### Code

	public static int countMyAnswer(String exp, boolean result) {
		if (exp.length() == 1) {
			return convertIntToBool(exp.charAt(0)) == result ? 1 : 0;
		}
		// eg. 1^0|0|1
		// result: true
		int totalCount = 0;
		for (int i = 1; i < exp.length(); i += 2) {

			char op = exp.charAt(i);
			String firstHalf = exp.substring(0, i);
			String secondHalf = exp.substring(i + 1);

			int firstHalfTrue = countMyAnswer(firstHalf, true);
			int firstHalfFalse = countMyAnswer(firstHalf, false);
			int secondHalfTrue = countMyAnswer(secondHalf, true);
			int secondHalfFalse = countMyAnswer(secondHalf, false);

			if (evaluate('0', op, '0') == result) {
				totalCount += firstHalfFalse * secondHalfFalse;
			}
			if (evaluate('0', op, '1') == result) {
				totalCount += firstHalfFalse * secondHalfTrue;
			}
			if (evaluate('1', op, '0') == result) {
				totalCount += firstHalfTrue * secondHalfFalse;
			}
			if (evaluate('1', op, '1') == result) {
				totalCount += firstHalfTrue * secondHalfTrue;
			}
		}
		return totalCount;
	}

	private static boolean convertIntToBool(char num) {
		if (num == '1') {
			return true;
		} else {
			return false;
		}
	}

	private static boolean evaluate(char num1, char op, char num2) {
		boolean b1 = convertIntToBool(num1);
		boolean b2 = convertIntToBool(num2);
		if (op == '&') {
			return b1 & b2;
		} else if (op == '|') {
			return b1 | b2;
		} else if (op == '^') {
			return b1 ^ b2;
		}
		System.out.println("Did not found operator " + op);
		return false;
	}
