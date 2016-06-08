---
layout: post
title: "[LeetCode 23] Merge k Sorted Lists "
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/merge-k-sorted-lists/)

<div class="question-content">
            <p></p><p>
Merge <i>k</i> sorted linked lists and return it as one sorted list. Analyze and describe its complexity.
</p><p></p>
</div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

There are two ways to solve this problem. 

* k - number of lists
* n - length of each list

__First approach is merge sort__. Using divide and conquer approach, divide the entire input into halves, and then merge 2 list each time. Instead of merging 1 by 1 which the time complexity is O(nk x (k-1)), the 2 lists to be merged is always similar length, thus time complexity is reduced to O(nk x logk). 

__You may wonder how I calculate time complexity__. See, each round of sort, nk nodes are read and sorted. This happened O(logk) times, where k is the number of lists. Thus totoal time take is O(nk x logk). 

__Second approach is heap sort__. The idea of this is to always keep a sorted list of the head of each list. When we retrieve items from the heap, it only take O(logk) time to find the next smallest element. 

Not sure what is a heap? Read __[Fundamental] Heap (data structure)__ before you proceed. 

Both method are well explained in [this csdn blog](http://blog.csdn.net/linhuanmars/article/details/19899259). Time complexity analysis is given by [nootcoder blog](http://n00tc0d3r.blogspot.sg/2013/04/merge-k-sorted-lists.html). 

### Solution

Divide and conquer code is lengthy but medium difficulty. 

Second solution, however, is not as easy. __Especially when we have to write Comparator on our own__.  A priority queue (heap) is implemented and head of each list is inserted into the heap. Then poll elements out from the heap until heap is empty. 

### My code 

__Merge sort code, written by me__

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
        public ListNode mergeKLists(List<ListNode> lists) {
            if (lists == null || lists.size() == 0) {
                return null;
            }
            return mergeHelper(lists, 0, lists.size() - 1);
        }

        private ListNode mergeHelper(List<ListNode> lists, int start, int end) {
            if (start == end) {
                return lists.get(start);
            } 
            int mid = start + (end - start) / 2;
            ListNode firstHalf = mergeHelper(lists, start, mid);
            ListNode secondHalf = mergeHelper(lists, mid + 1, end);
            return mergeTwo(firstHalf, secondHalf);
        }

        private ListNode mergeTwo(ListNode head1, ListNode head2) {
            ListNode dummy = new ListNode(0);
            ListNode p = dummy;
            while (head1 != null && head2 != null) {
                if (head1.val < head2.val) {
                    p.next = head1;
                    head1 = head1.next;
                    p = p.next;
                } else {
                    p.next = head2;
                    head2 = head2.next;
                    p = p.next;
                }
            }
            if (head1 == null) {
                p.next = head2;
            } else {
                p.next = head1;
            }
            return dummy.next;
        }
    }

__Heap sort code, written by me__. [source](http://answer.ninechapter.com/solutions/merge-k-sorted-lists/)

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
        public ListNode mergeKLists(List<ListNode> lists) {
            if (lists == null || lists.size() == 0) {
                return null;
            }
            int size = lists.size();
            // create a heap with Java priority queue, set the initial size
            Queue<ListNode> heap = new PriorityQueue(size, new NodeComparator());
            // add all ListNode into the heap
            for (ListNode node: lists) {
                if (node != null) {
                    heap.add(node);
                }
            }
            // start to link nodes from smallest to largest
            ListNode dummy = new ListNode(0);
            ListNode p = dummy;
            while (!heap.isEmpty()) {
                p.next = heap.remove();
                p = p.next;
                if (p.next != null) {
                    heap.add(p.next);
                }
            }
            return dummy.next;
        }

        class NodeComparator implements Comparator<ListNode> {
            public int compare(ListNode n1, ListNode n2) {
                return n1.val - n2.val;
            }
        }
    }
