---
layout: post
title: "[LeetCode 25] Reverse Nodes in k-Groups "
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/reverse-nodes-in-k-group/)

<div class="question-content">
<p></p><p>
Given a linked list, reverse the nodes of a linked list <i>k</i> at a time and return its modified list.
</p>

<p>
If the number of nodes is not a multiple of <i>k</i> then left-out nodes in the end should remain as it is.</p>

<p>You may not alter the values in the nodes, only nodes itself may be changed.</p>

<p>Only constant memory is allowed.</p>

<p>
For example,<br>
Given this linked list: <code>1-&gt;2-&gt;3-&gt;4-&gt;5</code>
</p>

<p>
For <i>k</i> = 2, you should return: <code>2-&gt;1-&gt;4-&gt;3-&gt;5</code>
</p>

<p>
For <i>k</i> = 3, you should return: <code>3-&gt;2-&gt;1-&gt;4-&gt;5</code>
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
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__The problem is solved in 2 steps__. First, get the next k-group. If remaining items is less than k, terminate the program. Otherwise, reserve this k-group and keep going. 

To solve this question is very tricky. __We need to be clear about this: 4 nodes need to be kept track of__: 2 elements before and after the k-group, and 2 elements within the k-group. 

__The difficult point is while and after reverse the k-group__, how to maintain the 'pre' node and future 'pre' node correctly. 

### Solution

Use Linkedlist Template from NineChap to solve. 

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
        public ListNode reverseKGroup(ListNode head, int k) {
            if (k <= 1 || head == null) {
                return head;
            }
            ListNode nextGroup = head;
            for (int i = 0; i < k; i++) {
                if (nextGroup == null) {
                    // there isn't k nodes in this list
                    return head;
                }
                nextGroup = nextGroup.next;
            }
            // now we're sure the list have at least k nodes
            // reverse this list (by re-connecting the next pointer k times)
            ListNode newHead = head;
            ListNode tail = null;
            for (int i = 0; i < k; i++) {
                ListNode temp = newHead.next;
                newHead.next = tail;
                tail = newHead;
                newHead = temp;
            }
            // now newHead is pointing to the actual new head
            // temp (which is not accessable here) is same as nextGroup
            // last step, reconnect everything and call recursion method
            head.next = reverseKGroup(nextGroup, k);
            return tail;
        }
    }
