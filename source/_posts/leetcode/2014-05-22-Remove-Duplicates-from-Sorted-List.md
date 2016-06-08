---
layout: post
title: "[LeetCode 83] Remove Duplicates from Sorted List"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/remove-duplicates-from-sorted-list/)

<div class="question-content">
            <p></p><p>
Given a sorted linked list, delete all duplicates such that each element appear only <i>once</i>.
</p>
<p>
For example,<br>
Given <code>1-&gt;1-&gt;2</code>, return <code>1-&gt;2</code>.<br>
Given <code>1-&gt;1-&gt;2-&gt;3-&gt;3</code>, return <code>1-&gt;2-&gt;3</code>.
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
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="white">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This question is trivial.__ The next following up question is not easy. 

### Code

__my code__

    public ListNode deleteDuplicates(ListNode head) {
        if (head == null) return null;
        ListNode pre = head;
        ListNode post = head;
        while (post != null){
            post = post.next;
            if (post == null || pre.val != post.val){
                pre.next = post;
                pre = post;
            }
        }
        return head;
    }