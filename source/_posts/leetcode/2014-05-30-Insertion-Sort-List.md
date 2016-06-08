---
layout: post
title: "[LeetCode 147] Insertion Sort List"
comments: true
category: Leetcode

---


### Question 
[link](http://oj.leetcode.com/problems/insertion-sort-list/)

<div class="question-content">
            <p></p><p>Sort a linked list using insertion sort.</p><p></p>
          </div>

### Stats
<table border="2">
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

### Analysis

__This question is a little tricky, but not difficult__. First important thing is to konw what is [insertion sort](http://en.wikipedia.org/wiki/Insertion_sort). It is always keeping a sorted list, and then get next unsorted element and insert into correct position of the sorted list. 

### Solution

__Almost all solutions on internet is same, so I will just explain my code__. My code can be optimized a little bit by studying [this blog](http://blog.csdn.net/linhuanmars/article/details/21144553), but I guess it's just refactoring 1 or 2 variables and execution time would not be affected.

My solution is dividing the list into 2 parts: sorted part and unsorted part. __I keep getting next node from unsorted and insert into sorted__. 

### My code 

Recursion: 

    public ListNode insertionSortList(ListNode head) {
        if (head == null || head.next == null) return head;
        ListNode sorted = new ListNode(Integer.MIN_VALUE);
        sorted.next = head;
        ListNode unsort = head.next;
        head.next = null;
        // the sorted and unsort both are not null at this point
        while (unsort != null) {
            ListNode pos = sorted;
            ListNode cur = unsort;
            unsort = unsort.next;
            while (pos.next != null && pos.val < cur.val 
                && pos.next.val < cur.val) pos = pos.next;
            // now insert (cur) to (pos.next)
            cur.next = pos.next;
            pos.next = cur;
        }
        return sorted.next;
    }

__Updated on June 17th, rewrote the code with dummy head__. This is different solution, with better readability. 

    public ListNode insertionSortList(ListNode head) {
        if (head == null) {
            return null;
        }
        ListNode dummy = new ListNode(0);
        ListNode cur = head;
        while (cur != null) {
            // insert cur into correct pos
            ListNode pos = dummy;
            while (pos.next != null && pos.next.val < cur.val) {
                pos = pos.next;
            }
            ListNode temp = cur.next;
            cur.next = pos.next;
            pos.next = cur;
            cur = temp;
        }
        return dummy.next;
    }
