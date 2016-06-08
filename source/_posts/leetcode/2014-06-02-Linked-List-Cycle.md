---
layout: post
title: "[LeetCode 141] Linked List Cycle"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/linked-list-cycle/)

<div class="question-content bg-color bg-img font-color">
            <p class="font-color"></p><p class="font-color">
Given a linked list, determine if it has a cycle in it.
</p>

<p class="font-color">
Follow up:<br>
Can you solve it without using extra space?
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

__This is an famous question, historically know as the [Tortoise and hare](http://en.wikipedia.org/wiki/Cycle_detection#Tortoise_and_hare)__. 

### Solution

[This blog](http://www.programcreek.com/2012/12/leetcode-linked-list-cycle/) has a great solution. 

> Use fast and low pointer. The advantage about fast/slow pointers is that when a circle is located, the fast one will catch the slow one for sure.

### Code

    public boolean hasCycle(ListNode head) {
        if (head == null || head.next == null) 
			return false;
		ListNode first = head.next, second = first.next;
		while (first != null && second != null) {
			if (first == second) return true;
			first = first.next;
			second = second.next;
			if (second == null) return false;
			second = second.next;
		}
		return false;
    }
