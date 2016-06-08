---
layout: post
title: "[CC150v5] 2.7 Linked List Palindrome "
comments: true
category: CC150v5
tags: [ src ]
---

### Question

> Implement a function to check if a linked list is a palindrome. 

### Solution

There are multiple solutions for this question. 

__First, maybe the simplest solution of all__, is to compare the list with the reversed list (compare first half would be enough). This is a very nice idea. 

__Second solution is iterative approach to use a Stack__. Alternatively, we can also use __fast/slow pointer__ to find the mid point. 

__Third solution is recursive__. We basically uses a public pointer to: 

1. get starting value
1. check middle parts
1. get ending value
1. if starting == ending and middle part is valid, then true.

This code is pretty hard to think. Read it below. 

### Code

Recursive

	private static LinkedListNode p;

	public static boolean isPalindromeRecursive(LinkedListNode head) {
		p = head;
		int len = getListLength(head);
		return recursiveHelper(0, len - 1);
	}

	private static int getListLength(LinkedListNode node) {
		int count = 0;
		while (node != null) {
			count++;
			node = node.next;
		}
		return count;
	}

	public static boolean recursiveHelper(int from, int to) {
		if (from > to) {
			return true;
		} else if (from == to) {
			p = p.next;
			return true;
		} else {
			// first get fromVal, then check middle part, last, get toVal
			int fromVal = p.data;
			p = p.next;
			if (!recursiveHelper(from + 1, to - 1)) {
				return false;
			}
			int toVal = p.data;
			p = p.next;
			if (fromVal != toVal) {
				return false;
			}
		}
		return true;
	}
