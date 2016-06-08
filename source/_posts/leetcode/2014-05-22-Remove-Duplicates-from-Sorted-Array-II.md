---
layout: post
title: "[LeetCode 80] Remove Duplicates from Sorted Array II"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/remove-duplicates-from-sorted-array-ii/)

<div class="question-content">
            <p></p><p>
Follow up for "Remove Duplicates":<br>
What if duplicates are allowed at most <i>twice</i>?</p>

<p>
For example,<br>
Given sorted array A = <code>[1,1,1,2,2,3]</code>,
</p>
<p>
Your function should return length = <code>5</code>, and A is now <code>[1,1,2,2,3]</code>.
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

### Analysis

__This is an easy question__

### Code

__my first code__

    public int removeDuplicates(int[] A) {
        if (A.length == 0) return 0;
        int insert = 1, pre = 0, cur = 1, count = 1;
        while (cur < A.length) {
            if (A[pre] == A[cur]) {
                if (count == 1) {
                    count = 2;
                    A[insert] = A[pre];
                    insert++;
                    pre++;
                }
            } else if (A[pre] != A[cur]) {
                count = 1;
                A[insert++] = A[cur];
                pre = cur;
            }
            cur ++;
        }
        return insert;
    }

__my second code__

    public int removeDuplicates(int[] A) {
        int len = A.length;
        if (len < 3) return len;
        int left = 0, right = 0;
        boolean dup = false;
        while (right < len) {
            if (right == 0 || A[right] != A[right - 1]) {
                A[left ++] = A[right ++];
                dup = false;
            } else if (! dup) {
                A[left ++] = A[right ++];
                dup = true;
            } else right ++;
        }
        return left;
    }