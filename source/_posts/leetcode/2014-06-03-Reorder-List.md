---
layout: post
title: "[LeetCode 143] Reorder List"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/reorder-list/)

<div class="question-content bg-color bg-img font-color">
            <p class="font-color"></p><p class="font-color">
Given a singly linked list <i>L</i>: <i>L</i><sub>0</sub>→<i>L</i><sub>1</sub>→…→<i>L</i><sub><i>n</i>-1</sub>→<i>L</i><sub>n</sub>,<br>
reorder it to: <i>L</i><sub>0</sub>→<i>L</i><sub><i>n</i></sub>→<i>L</i><sub>1</sub>→<i>L</i><sub><i>n</i>-1</sub>→<i>L</i><sub>2</sub>→<i>L</i><sub><i>n</i>-2</sub>→…
</p>

<p class="font-color">You must do this in-place without altering the nodes' values.</p>

<p class="font-color">
For example,<br>
Given <code>{1,2,3,4}</code>, reorder it to <code>{1,4,2,3}</code>.
</p><p class="font-color"></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a difficult question to think__. 

I first solved it with an stack which stores the second half nodes. It works. However, IT IS NOT A IN-PLACE SOLUTION, thus it's wrong. 

Eventually I did not solve it. 

__There is only one standard solution from the Internet__. [This blog](http://www.programcreek.com/2013/12/in-place-reorder-a-singly-linked-list-in-java/) explains it. 

> 1. Break list in the middle to two lists (use fast & slow pointers)
> 2. Reverse the order of the second list
> 3. Merge two list back together

Simple, right? __Because of the nature of linked list, a lot of things can be done in-place__, so we need not use any other data strucutres. 

### Solution

The code is a bit lengthy and difficult to write. It took me a while, but passed in 1 go. 

### Code

__First, code written by me__

    public void reorderList(ListNode head) {
        if (head == null || head.next == null) {
			return;
		}
		ListNode slow = head, fast = head;
		while (fast != null) {
			if (fast.next != null && fast.next.next != null) {
				fast = fast.next.next;
				slow = slow.next;
			}
			else {
				fast = null;
			}
		}
		// if length = 2, slow point to 1st
		// if length = 3, slow point to 2nd
		// if length = 4, slow point to 2nd
		ListNode secondHalf = slow.next;
		slow.next = null;
		// now reverse secondHalf
		ListNode p = secondHalf;
		while (p.next != null) {
			ListNode tail = p.next.next;
			p.next.next = secondHalf;
			secondHalf = p.next;
			p.next = tail;
		}
		// now merge 2 list: head and secondHalf
		ListNode a = head, b = secondHalf;
		while (a != null && b != null) {
			ListNode temp1 = a.next;
			ListNode temp2 = b.next;
			a.next = b;
			b.next = temp1;
			a = temp1;
			b = temp2;
		}
    }

__Second, code written by [someone](https://oj.leetcode.com/discuss/236/does-this-problem-solution-time-complexity-space-comlexity)__

    public void reorderList(ListNode head) {
        // IMPORTANT: Please reset any member data you declared, as
        // the same Solution instance will be reused for each test case.
        if (head == null || head.next == null) return;
        ListNode fast = head;
        ListNode slow = head;
        while(fast != null && fast.next != null) {
            fast = fast.next.next;
            slow = slow.next;
        }
        ListNode reverseHead = slow.next;           // find the second half of list
        slow.next = null;                           // make first half end point to null
        reverseHead = reverse(reverseHead);         // reverse second half     
        ListNode cur = head;        
        while(reverseHead != null) {                // link together
            ListNode tmp = reverseHead.next;
            reverseHead.next = cur.next;
            cur.next = reverseHead;
            cur = cur.next.next;
            reverseHead = tmp;
        }
    }
    private ListNode reverse(ListNode head) {
        if (head == null || head.next == null) return head;
        ListNode prev = new ListNode(0);
        prev.next = head;
        head = prev;
        ListNode cur = prev.next;
        while(cur.next != null) {
            ListNode tmp = cur.next;
            cur.next = tmp.next;
            tmp.next = prev.next;
            prev.next = tmp;
        }
        return prev.next;
    }
