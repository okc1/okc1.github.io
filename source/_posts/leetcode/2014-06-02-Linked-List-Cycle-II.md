---
layout: post
title: "[LeetCode 142] Linked List Cycle II"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/linked-list-cycle-ii/)

<div class="question-content bg-color bg-img font-color">
            <p class="font-color"></p><p class="font-color">
Given a linked list, return the node where the cycle begins. If there is no cycle, return <code>null</code>.
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
		<td bgcolor="red">5</td>
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

[This blog](http://fisherlei.blogspot.sg/2013/11/leetcode-linked-list-cycle-ii-solution.html
) has a great solution. 

<blockquote cite="">
    <p class="font-color">现在有两个指针，第一个指针，每走一次走一步，第二个指针每走一次走两步，如果他们走了t次之后相遇在K点</p>
    <p class="font-color">那么&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 指针一&nbsp; 走的路是&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; t = X + nY + K&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ①</p>
    <p class="font-color">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 指针二&nbsp; 走的路是&nbsp;&nbsp;&nbsp;&nbsp; 2t = X + mY+ K&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ②&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; m,n为未知数</p>
    <p class="font-color">把等式一代入到等式二中, 有</p>
    <p class="font-color">2X + 2nY + 2K = X + mY + K</p>
    <p class="font-color">=&gt;&nbsp;&nbsp; X+K&nbsp; =&nbsp; (m-2n)Y&nbsp;&nbsp;&nbsp; ③</p>
    <p class="font-color">这就清晰了，X和K的关系是基于Y互补的。等于说，两个指针相遇以后，再往下走X步就回到Cycle的起点了。这就可以有O(n)的实现了。</p>
</blockquote>

{% img middle /assets/images/Linked-List-Cycle-II.png %}

### Code

    public ListNode detectCycle(ListNode head) {
        if (head == null || head.next == null) 
			return null;
		ListNode first = head.next, second = first.next;
		ListNode found = null;
		while (first != null && second != null) {
			if (first == second) {
			    found = first;
			    break;
			}
			first = first.next;
			second = second.next;
			if (second == null) break;
			second = second.next;
		}
		if (found == null) return null;
		first = head;
		while (first != second) {
			first = first.next;
			second = second.next;
		}
		return first;
    }
