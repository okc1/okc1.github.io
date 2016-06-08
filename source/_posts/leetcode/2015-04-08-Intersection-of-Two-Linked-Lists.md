---
layout: post
title: "[LeetCode 160] Intersection of Two Linked Lists "
comments: true
category: Leetcode
---

### Question 

[link](https://leetcode.com/problems/intersection-of-two-linked-lists/)

<div class="question-content">
              <p></p><p>Write a program to find the node at which the intersection of two singly linked lists begins.</p>
<br>
<p>For example, the following two linked lists: </p>
<pre>A:          a1 ? a2
                   ?
                     c1 ? c2 ? c3
                   ?            
B:     b1 ? b2 ? b3
</pre>
<p>begin to intersect at node c1.</p>
<br>
<p><b>Notes:</b>
</p><ul>
<li>If the two linked lists have no intersection at all, return <code>null</code>.</li>
<li>The linked lists must retain their original structure after the function returns. </li>
<li>You may assume there are no cycles anywhere in the entire linked structure.</li>
<li>Your code should preferably run in O(n) time and use only O(1) memory.</li>
</ul>
<p></p>

<p><b>Credits:</b><br>Special thanks to <a href="https://oj.leetcode.com/discuss/user/stellari">@stellari</a> for adding this problem and creating all test cases.</p><p></p>
              
                <div id="tags" class="btn btn-xs btn-warning">Show Tags</div>
                <span class="hide">
                  
                  <a class="btn btn-xs btn-primary" href="/tag/linked-list/">Linked List</a>
                  
                </span>
              
            </div>

### Analysis

This question is very similar to __[LeetCode Plus] Lowest Common Ancestor of Binary Tree (II)__. 

### Solution

[This](http://stackoverflow.com/a/2216683/909524) is a pretty nice answer. The following explanation is quoted from [g4g](http://www.geeksforgeeks.org/write-a-function-to-get-the-intersection-point-of-two-linked-lists/):

>1. Get count of the nodes in first list, let count be c1.
>
>2. Get count of the nodes in second list, let count be c2.
>
>3. Get the difference of counts d = abs(c1 – c2)
>
>4. Now traverse the bigger list from the first node till d nodes so that from here onwards both the lists have equal no of nodes.
>
>5. Then we can traverse both the lists in parallel till we come across a common node. 

### Code

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
        public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
            return helper(headA, headB, length(headA) - length(headB));
        }

        public ListNode helper(ListNode n1, ListNode n2, int offset) {
            if (offset < 0) {
                return helper(n2, n1, 0 - offset);
            }
            // move n1 to the distance of offset
            while (offset != 0) {
                n1 = n1.next;
                offset--;
            }
            while (n1 != null && n1 != n2) {
                n1 = n1.next;
                n2 = n2.next;
            }
            return n1;
        }

        int length(ListNode node) {
            int len = 0;
            while (node != null) {
                node = node.next;
                len++;
            }
            return len;
        }
    }
