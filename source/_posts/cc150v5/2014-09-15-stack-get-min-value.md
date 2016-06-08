---
layout: post
title: "[CC150v5] 3.2 Stack Min Value "
comments: true
category: CC150v5
tags: [ src ]
---

### Question

> How would you design a stack which, in addition to push and pop, also has a function min which returns the minimum element? 

> Push, pop and min should all operate in 0(1) time. 

### Solution

This is __a very tricky question__. 

The key is how to use the minimum space to achieve O(1) query min operation. The trick is to count how many times the same min-value occur. Eg. 

> input: 5,3,3,1,1,2,2,2,2,2,2,2.
>
> stack: 5,3,3,1,1.

So we can pop '1' twice, pop '3' twice, and pop '5' once. Read the code! 

### Code

	public class StackMyAnswer extends Stack<Integer> {

		Stack<Integer> min = new Stack<Integer>();

		public void push(int value) {
			if (min.isEmpty() || value <= min.peek()) {
				min.push(value);
			}
			super.push(value);
		}

		public Integer pop() {
			int val = super.pop();
			if (!min.isEmpty() && val == min.peek()) {
				min.pop();
			}
			return val;
		}

		public int min() {
			if (min.isEmpty()) {
				return Integer.MAX_VALUE;
			}
			return min.peek();
		}
	}
