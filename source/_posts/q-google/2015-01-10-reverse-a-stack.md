---
layout: post
title: "[Google] Reverse a Stack without DS "
comments: true
category: q-google
tags: [ src ]
---

### Question 

[link](http://www.geeksforgeeks.org/reverse-a-stack-using-recursion/)

> Reverse a stack using recursion. You are not allowed to use loops or data structure, and you can only use the following functions:

    isEmpty(S)
    push(S)
    pop(S)

### Solution

Well since we are not allowed to use additional DS or loop, we have to use system stack to help us! 

We add a new method: __insert at stack bottom__. Then we can solve this question recursively. Nice question, and tricky answer! 

### Code

	public void reverse(Stack<Integer> stack) {
		if (stack.isEmpty() || stack.size() == 1) {
			return;
		}
		int top = stack.pop();
		this.reverse(stack);
		this.insertAtBottom(stack, top);
	}

	private void insertAtBottom(Stack<Integer> stack, int val) {
		if (stack.isEmpty()) {
			stack.push(val);
			return;
		}
		int temp = stack.pop();
		this.insertAtBottom(stack, val);
		stack.push(temp);
	}
