---
layout: post
title: "[LeetCode 2] Add Two Numbers"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/add-two-numbers/)

<div class="question-content">
    <p></p>
    <p>You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.</p>
    <p style="font-family:monospace">
    <b>Input:</b> (2 -&gt; 4 -&gt; 3) + (5 -&gt; 6 -&gt; 4)<br>
    <b>Output:</b> 7 -&gt; 0 -&gt; 8</p>
    <p></p>
</div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
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

### Solution

This question is straight-forward. Just add one by one with a carry bit. 

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
        public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
            return helper(l1, l2, 0);
        }

        private ListNode helper(ListNode l1, ListNode l2, int carry) {
            if (l1 == null && l2 == null) {
                if (carry == 0) {
                    return null;
                } else {
                    return new ListNode(1);
                }
            } else if (l1 == null) {
                return helper(new ListNode(0), l2, carry);
            } else if (l2 == null) {
                return helper(l1, new ListNode(0), carry);
            } else {
                // both l1 and l2 have value
                int sum = l1.val + l2.val + carry;
                int resultNumber = sum % 10;
                int newCarry = sum / 10;
                ListNode ans = new ListNode(resultNumber);
                ans.next = helper(l1.next, l2.next, newCarry);
                return ans;
            }
        }
    }

Instead of doing it recursively, someone write a nice code for an iterative [solution](http://gongxuns.blogspot.sg/2012/12/leetcodeadd-two-numbers.html)

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
        public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
            int carry = 0;
            ListNode res = new ListNode(0);
            ListNode cur1 = l1, cur2 = l2, head = res;
            while (cur1 != null || cur2 != null) {
                if (cur1 != null) {
                    carry += cur1.val;
                    cur1 = cur1.next;
                }
                if (cur2 != null) {
                    carry += cur2.val;
                    cur2 = cur2.next;
                }
                head.next = new ListNode(carry % 10);
                head = head.next;
                carry /= 10;
            }
            if (carry == 1)
                head.next = new ListNode(1);
            return res.next;
        }
    }
