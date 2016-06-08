---
layout: post
title: "[LeetCode 82] Remove Duplicates from Sorted List II"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/remove-duplicates-from-sorted-list-ii/)

<div class="question-content">
            <p></p><p>
Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only <i>distinct</i> numbers from the original list.
</p>
<p>
For example,<br>
Given <code>1-&gt;2-&gt;3-&gt;3-&gt;4-&gt;4-&gt;5</code>, return <code>1-&gt;2-&gt;5</code>.<br>
Given <code>1-&gt;1-&gt;1-&gt;2-&gt;3</code>, return <code>2-&gt;3</code>.
</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a very important question__. Solution is a little tricky with boundary cases that need consider. 

My code works, but there is an __extremely good solution__ posted below. 

### Code

__First, my code__

    public ListNode deleteDuplicates(ListNode head) {
        ListNode preHead = new ListNode(0);
        preHead.next = head;
        ListNode left = preHead, right = head;
        while (right != null) {
            if (right.next == null || right.val != right.next.val) {
                // next is differnet from previous
                left = right;
                right = right.next;
            }
            else {
                // next is same as previous
                while (right.next != null && right.val == right.next.val) 
                    right = right.next;
                left.next = right.next;
                right = right.next;
            }
        }
        return preHead.next;
    }

__Second, a great solution from [this blog](http://codeganker.blogspot.sg/2014/04/remove-duplicates-from-sorted-list-ii.html).__

    public ListNode deleteDuplicates(ListNode head) {
        if(head == null) return head;
        ListNode helper = new ListNode(0);
        helper.next = head;
        ListNode pre = helper, cur = head;
        while(cur!=null)
        {
            while(cur.next!=null && pre.next.val==cur.next.val)
                cur = cur.next;
            if (pre.next == cur) 
                pre = pre.next;
            else 
                pre.next = cur.next;
            cur = cur.next;
        }
        return helper.next;
    }