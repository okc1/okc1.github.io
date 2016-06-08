---
layout: post
title: "[LeetCode 92] Reverse Linked List II"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/reverse-linked-list-ii/)

<div class="question-content">
            <p></p><p>
Reverse a linked list from position <i>m</i> to <i>n</i>. Do it in-place and in one-pass.
</p>

<p>
For example:<br>
Given <code>1-&gt;2-&gt;3-&gt;4-&gt;5-&gt;NULL</code>, <i>m</i> = 2 and <i>n</i> = 4,
</p>
<p>
return <code>1-&gt;4-&gt;3-&gt;2-&gt;5-&gt;NULL</code>.
</p>
<p>
<b>Note:</b><br>
Given <i>m</i>, <i>n</i> satisfy the following condition:<br>
1 ≤ <i>m</i> ≤ <i>n</i> ≤ length of list.
</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a very standard interview question of LinkedList__. 

### Solution

__Keep 2 pointers, one of which points to preReversePosition, another one points to finalTailOfTheReversedPart__. Each time, I will get next element and insert it between the 2 pointers mentioned above. See below image for details: 

{% img middle /assets/images/reverse-linked-list-ii.png %}

The coding isn't easy, there can be a lot of details being omitted. Just think of it in this way: in the above picture, 123 is broken away from 45678. Each time, get next element from 45678, and insert it right after 2. Do this 2 times, so that 4,5 are moved. In the end, make 3 point to 6, and solution done. 

### Code

__First, my code__

    public ListNode reverseBetween(ListNode head, int m, int n) {
        ListNode preHead = new ListNode(0);
        preHead.next = head;
        ListNode before = preHead;
        for (int i = 1; i < m; i ++)
            before = before.next;
        ListNode rTail = before.next;
        ListNode cur = before.next.next;
        for (int i = 0; i < n - m; i ++) {
            ListNode temp = cur.next;
            cur.next = before.next;
            before.next = cur;
            cur = temp;
        }
        rTail.next = cur;
        return preHead.next;
    }

__Second, __

A lot of people have similar solutions, so I won't post any of their code. Reading it won't help, write it yourself is actually important. 

A lot of people have complained about this problem not easy to write. 