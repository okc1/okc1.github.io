---
layout: post
title: "[LeetCode 35] Search Insert Position "
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/search-insert-position/)

<div class="question-content">
            <p></p><p>Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.</p>

<p>You may assume no duplicates in the array.</p>

<p>
Here are few examples.<br>
<code>[1,3,5,6]</code>, 5 → 2<br>
<code>[1,3,5,6]</code>, 2 → 1<br>
<code>[1,3,5,6]</code>, 7 → 4<br>
<code>[1,3,5,6]</code>, 0 → 0
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
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a very basic, yet very difficult question__. It is not easy to get it correct at first attempt.

Read [this blog](http://blog.csdn.net/fightforyourdream/article/details/14216321) for more. 

### My code 

    public class Solution {
        public int searchInsert(int[] A, int target) {
            if (A == null || A.length == 0) {
                return 0;
            }
            int len = A.length;
            int left = 0;
            int right = len - 1;
            while (left + 1 < right) {
                int mid = left + (right - left) / 2;
                if (A[mid] >= target) {
                    right = mid;
                } else {
                    left = mid;
                }
            }
            // now are have a adjacent range [left, right]
            if (target <= A[left]) {
                return left;
            } else if (target <= A[right]) {
                // remember not to miss the == case
                return right;
            } else {
                return right + 1;
            }
        }
    }
