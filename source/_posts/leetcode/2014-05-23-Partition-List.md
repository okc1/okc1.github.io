---
layout: post
title: "[LeetCode 86] Partition List"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/partition-list/)

<div class="question-content">
            <p></p><p>Given a linked list and a value <i>x</i>, partition it such that all nodes less than <i>x</i> come before nodes greater than or equal to <i>x</i>.
</p>
<p>
You should preserve the original relative order of the nodes in each of the two partitions.
</p>
<p>
For example,<br>
Given <code>1-&gt;4-&gt;3-&gt;2-&gt;5-&gt;2</code> and <i>x</i> = 3,<br>
return <code>1-&gt;2-&gt;2-&gt;4-&gt;3-&gt;5</code>.
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
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This question is not very difficult__, but can be confusing if the code don't have good logic. 

### Solution

There is no fancy algorithm solution. I got it wrong in 10 submissions at first. After a few days, I did this problem again and passed with 1 attempt. 

So just keep practicing. 

### Code

__my code__

    public ListNode partition(ListNode head, int x) {
        if (head == null) return head;
        ListNode PH = new ListNode(1);
        PH.next = head;
        ListNode left = PH, preRight = PH, right = head;
        while (right != null) {
            if (right.val < x) {
                if (preRight != left) {
                    preRight.next = right.next;
                    right.next = left.next;
                    left.next = right;
                    left = right;
                    right = preRight.next;
                } else {
                    left = left.next;
                    preRight = left;
                    right = right.next;
                }
            } else {
                preRight = right;
                right = preRight.next;
            }
        }
        return PH.next;
    }
