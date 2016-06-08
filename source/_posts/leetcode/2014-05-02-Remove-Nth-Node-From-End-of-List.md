---
layout: post
title: "[LeetCode 19] Remove Nth Node From End of List"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/remove-nth-node-from-end-of-list/)

<div class="question-content">
            <p></p><p>Given a linked list, remove the <i>n</i><sup>th</sup> node from the end of list and return its head.</p>

<p>
For example,</p>

<pre>   Given linked list: <b>1-&gt;2-&gt;3-&gt;4-&gt;5</b>, and <b><i>n</i> = 2</b>.

   After removing the second node from the end, the linked list becomes <b>1-&gt;2-&gt;3-&gt;5</b>.
</pre>

<p>
<b>Note:</b><br>
Given <i>n</i> will always be valid.<br>
Try to do this in one pass.
</p><p></p>
          </div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

Note the special case: if the head node needs to be removed! 

### Solution

The code explains itself. Just don't forget the special cases. 

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
        public ListNode removeNthFromEnd(ListNode head, int n) {
            if (head == null) {
                return null;
            }
            ListNode left = head;
            ListNode right = head;
            // important to note that head node can be removed as well!
            // advance right pointer now
            for (int i = 0; i < n; i++) {
                right = right.next;
                if (right == null) {
                    right = head;
                }
            }
            // advance left and right pointer together
            while (right.next != null) {
                left = left.next;
                right = right.next;
            }
            // remove the node after left pointer
            // again, the below error check is not necessary
            if (left.next == null) {
                // need to remove the header in this case
                return head.next;
            } else {
                left.next = left.next.next;
                return head;
            }
        }
    }
