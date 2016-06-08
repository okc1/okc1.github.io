---
layout: post
title: "[CC150v5] 2.2 Kth last element (recursive) "
comments: true
category: CC150v5

---

### Question

> Implement an algorithm to find the kth to last element of a singly linked list.

> Do it recursively.

### Solution

Iterative solution is easy, __recursive is not__. 

### Code

	public static int nthToLastRecursive(LinkedListNode head, int n) {
		if (n == 0 || head == null) {
			return 0;
		}
		int k = nthToLastRecursive(head.next, n) + 1;
		if (k == n) {
			System.out.println(n + "th to last node is " + head.data);
		}
		return k;
	}
