---
layout: post
title: "[Question] Push and Pop Sequences of Stacks"
comments: true
category: Question

---

### Question 

[link](http://codercareer.blogspot.sg/2011/11/no-21-push-and-pop-sequences-of-stacks.html)

> Given two integer sequences, one of which is the push sequence of a stack, please check whether the other sequence is a corresponding pop sequence or not. 

> For example, if 1, 2, 3, 4, 5 is a push sequence, 4, 5, 3, 2, 1 is a corresponding pop sequence, but the sequence 4, 3, 5, 1, 2 is not.

### Solution

Refer to [this answer](http://stackoverflow.com/a/17828345): 

> Construct the stack: 
>
> For each number X in the pop order:

    If this number is not the same as the top of the stack (or the stack is empty), 
    push numbers from the push order until you pushed X. 
    
    If you pushed all numbers and didn't find X, there's no way to get the pop order.
    
    Pop X

### Code

	public boolean validSequence(int[] input, int[] sequenc) {
		// keep a pointer p in the input[] array
		int len = input.length;
		int p = 0;
		Stack<Integer> stack = new Stack<Integer>();

		int i = 0;
		while (i < len) {
			if (stack.isEmpty()) {
				// just push an element to stack
				stack.push(input[p++]);
			} else {
				// stack got elements, then check top one
				if (stack.peek() == sequenc[i]) {
					// seq found, proceed to next number in seq
					stack.pop();
					i++;
				} else {
					// did not find seq, keep pushing to stack until done
					if (p == len) {
						return false;
					} else {
						stack.push(input[p++]);
					}
				}
			}
		}
		return i == len; // or just return true;
	}
