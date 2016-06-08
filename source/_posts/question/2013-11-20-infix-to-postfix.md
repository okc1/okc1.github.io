---
layout: post
title: "[Amazon] Infix to Postfix conversion "
comments: true
category: Question
tags: [  ]
---

# Question

[link](https://cs.nyu.edu/courses/Fall12/CSCI-GA.1133-002/notes/InfixToPostfixExamples.pdf), [link](http://csis.pace.edu/~wolf/CS122/infix-postfix.htm).

> example: A * B + C becomes A B * C +

> A * (B + C) becomes A B C + *

# Solution

One of the main purpose of converting infix to postfix is to __remove alll parentheses__ from the expression. 

This is a very difficult question. The solution is:

1. Print operands as they arrive.

1. If the incoming symbol is '+' or '-' or '(', push it on the stack. 

1. If the incoming symbol is a ')', pop the stack and print the operators until you see a '('. Discard the pair of parentheses.

1. If the incoming symbol is '*' or '/', pop until we sees '+' or '-' or '(' at top of the stack, then push the symbol onto the stack. 

1. At the end of the expression, pop and print all operators on the stack. (No parentheses should remain.)

# Code

	public String solve(String infix) {
		StringBuilder sb = new StringBuilder();
		// get next operand or non-operand
		// notice that operand is >=1 chars
		int p = 0;
		int len = infix.length();
		Stack<Character> stack = new Stack<Character>();

		while (p != len) {
			if (isDigit(infix.charAt(p))) {
				// if char at p is a digit
				int q = p;
				while (q != len && isDigit(infix.charAt(q))) {
					q++;
				}
				// it is a number in the range [p, q-1]
				sb.append(infix.substring(p, q) + " ");
				p = q;
			} else {
				// if char at p is + - * / or ( )
				char op = infix.charAt(p++);
				if (op == ')') {
					// pop until sees a '('
					while (stack.peek() != '(') {
						sb.append(stack.pop() + " ");
					}
					stack.pop();
				} else if (op == '(' || op == '+' || op == '-') {
					stack.push(op);
				} else {
					// if * or /
					// pop until sees + or - or '('
					while (!stack.isEmpty()) {
						if (stack.peek() == '+' || stack.peek() == '-' || stack.peek() == '(') {
							break;
						}
						sb.append(stack.pop() + " ");
					}
					stack.push(op);
				}
			}
		}
		// reach Eof, pop everything
		while (!stack.isEmpty()) {
			sb.append(stack.pop() + " ");
		}
		return sb.toString();
	}
