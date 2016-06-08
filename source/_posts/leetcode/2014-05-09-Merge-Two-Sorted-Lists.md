---
layout: post
title: "[LeetCode 21] Merge Two Sorted Lists "
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/merge-two-sorted-lists/)

<div class="question-content">
            <p></p><p>Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.</p><p></p>
          </div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="lime">2</td>
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

__This question is easy__. There are difficult ways to solve. 

### Solution

There are 2 ways to solve this problem. First and the easy one is to __do recursion__. 

Second solution, also my original solution is to __use a 'fakeHead' to help__. Read [this blog](http://www.programcreek.com/2012/12/leetcode-merge-two-sorted-lists-java/). 

### My code 

Recursion: 

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
        public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
            if (l1 == null) {
                return l2;
            } else if (l2 == null) {
                return l1;
            } else {
                if (l1.val < l2.val) {
                    l1.next = mergeTwoLists(l1.next, l2);
                    return l1;
                } else {
                    l2.next = mergeTwoLists(l1, l2.next);
                    return l2;
                }
            }
        }
    }

Temporary header + link operations

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
        public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
            ListNode pre = new ListNode(0);
            ListNode cur = pre;
            while (l1 != null && l2 != null) {
                if (l1.val < l2.val) {
                    cur.next = l1;
                    l1 = l1.next;
                } else {
                    cur.next = l2;
                    l2 = l2.next;
                }
                cur = cur.next;
            }
            if (l1 == null) cur.next = l2;
            else cur.next = l1;
            return pre.next;
        }
    }
