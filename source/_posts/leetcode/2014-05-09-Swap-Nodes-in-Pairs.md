---
layout: post
title: "[LeetCode 24] Swap Nodes in Pairs "
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/swap-nodes-in-pairs/)

<div class="question-content">
            <p></p><p>
Given a linked list, swap every two adjacent nodes and return its head.
</p>

<p>
For example,<br>
Given <code>1-&gt;2-&gt;3-&gt;4</code>, you should return the list as <code>2-&gt;1-&gt;4-&gt;3</code>.
</p>

<p>
Your algorithm should use only constant space. You may <b>not</b> modify the values in the list, only nodes itself can be changed.
</p><p></p>
</div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="lime">2</td>
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

### Solution

The easier solution is of course __recursion__. We only need to swap 2 nodes and then call the method recursively. Find code below. 

__However, there exists iterative solution, just slightly complex__. Read [here](http://oj.leetcode.com/discuss/3608/seeking-for-a-better-solution) for more. Two pieces of iterative code are posted below. 

### My code 

Recursion 

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
        public ListNode swapPairs(ListNode head) {
            if (head == null || head.next == null) {
                return head;
            }
            ListNode temp = head.next;
            head.next = swapPairs(temp.next);
            temp.next = head;
            return temp;
        }
    }

Iterative solution using while loop. [ref](http://gongxuns.blogspot.sg/2012/12/leetcodeswap-nodes-in-pairs.html)

    public ListNode swapPairs(ListNode head) {
    	if (head == null) return head;
    	ListNode preHead = new ListNode(1);
    	preHead.next = head;
    	ListNode cur = head, pre = preHead;
    	while (cur != null && cur.next != null) {
    		pre.next = cur.next;
    		ListNode newCur = cur.next.next;
    		cur.next.next = cur;
    		cur.next = newCur;
    		pre = cur;
    		cur = newCur;
    	}
    	return preHead.next;
    }

Iterative solution using for loop. [ref](http://oj.leetcode.com/discuss/3608/seeking-for-a-better-solution)

    public ListNode swapPairs(ListNode head) {
    	ListNode start = new ListNode(0);
    	start.next = head;
    	for (ListNode cur = start; cur.next != null 
    	       && cur.next.next != null; cur = cur.next.next) {
    		cur.next = swap(cur.next, cur.next.next);
    	}
    	return start.next;
    }

    private ListNode swap(ListNode next1, ListNode next2) {
    	next1.next = next2.next;
    	next2.next = next1;
    	return next2;
    }
