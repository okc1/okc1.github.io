---
layout: post
title: "[LeetCode 61] Rotate List"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/rotate-list/)

<div class="question-content">
            <p></p><p>Given a list, rotate the list to the right by <i>k</i> places, where <i>k</i> is non-negative.</p>

<p>For example:<br>
Given <code>1-&gt;2-&gt;3-&gt;4-&gt;5-&gt;NULL</code> and <i>k</i> = <code>2</code>,<br>
return <code>4-&gt;5-&gt;1-&gt;2-&gt;3-&gt;NULL</code>.</p><p></p>
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
		<td bgcolor="yellow">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Solution

__This is a very basic question, but not very easy__. 

The implementation is a lot of node operations. The rest of things is straight-forward.

Read [this blog](http://rleetcode.blogspot.sg/2014/01/rotate-list-java.html) for more. 

### My code

	/**
	 * Definition for singly-linked list.
	 * public class ListNode {
	 *     int val;
	 *     ListNode next;
	 *     ListNode(int x) {
	 *         val = x;
	 *         next = null;
	 *     }
	 * }
	 */
	public class Solution {
	    public ListNode rotateRight(ListNode head, int n) {
	        if (head == null) {
	            return null;
	        }
	        ListNode p = head;
	        for (int i = 0; i < n; i++) {
	            if (p.next != null) {
	                p = p.next;
	            } else {
	                p = head;
	            }
	        }
	        ListNode q = head;
	        while (p.next != null) {
	            p = p.next;
	            q = q.next;
	        }
	        if (q.next == null) {
	            return head;
	        }
	        ListNode newHead = q.next;
	        q.next = null;
	        p.next = head;
	        return newHead;
	    }
	}
