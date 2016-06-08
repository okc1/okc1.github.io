---
layout: post
title: "[LeetCode Plus] Reverse linked list iteratively and recursively"
comments: true
category: leetcode_plus
tags: [ unit test needed ]
---

### Question 

[link](http://leetcode.com/2010/04/reversing-linked-list-iteratively-and.html)

> Implement the reversal of a singly linked list iteratively and recursively. 

### Iteratively

First, the iterative solution is very common, and is listed as __one of the "5 fundamental operations of linked list"__ in the NineChap4 post. I will quote below. 

> First variant: Reverse from a particular node to the end

	public ListNode reverse(ListNode start) {
        ListNode result = null;
        ListNode cur = start;
        while (cur != null) {
            ListNode temp = cur.next;
            cur.next = result;
            result = cur;
            cur = temp;
        }
        return result;
	}

> Second variant: Reverse from a node until another node

	public ListNode reverseRange(ListNode start, int len) {
		ListNode result = null;
		ListNode cur = start;
		while (len > 0) {
			ListNode temp = cur.next;
			cur.next = result;
			result = cur;
			cur = temp;
			len--;
		}
		start.next = cur;
		return result;
	}


### Recursively

A good solution suggest by [this answer](http://stackoverflow.com/a/354937):

	public ListNode reverseRecursively(ListNode head) {
		if (head == null || head.next == null) {
			return head;
		}
		ListNode temp = head.next;
		// temp is not NULL
		ListNode newHead = reverseRecursively(temp);
		temp.next = head;
		head.next = null;
		return newHead;
	}
