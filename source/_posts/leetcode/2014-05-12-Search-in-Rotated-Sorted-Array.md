---
layout: post
title: "[LeetCode 33] Search in Rotated Sorted Array"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/search-in-rotated-sorted-array/)

<div class="question-content">
            <p></p><p>Suppose a sorted array is rotated at some pivot unknown to you beforehand.</p>

<p>(i.e., <code>0 1 2 4 5 6 7</code> might become <code>4 5 6 7 0 1 2</code>).</p>

<p>You are given a target value to search. If found in the array return its index, otherwise return -1.</p>

<p>You may assume no duplicate exists in the array.</p><p></p>
          </div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This question is not very difficult__, yet commonly seen in interviews. 

Without having any knowledge of pivot, we can check the mid-point value against left value and right value. Read [this blog](http://leetcode.com/2010/04/searching-element-in-rotated-array.html) for more.

### Solution

The code is easy to understand.

### My code 

Pay special attention to different larger/smaller conditions. It's very easy to miss a equal sign or something. 

    public class Solution {
        public int search(int[] A, int target) {
            if (A == null || A.length == 0) {
                return -1;
            }
            int len = A.length;
            int left = 0; 
            int right = len - 1;
            while (left + 1 < right) {
                int mid = left + (right - left) / 2;
                if (A[mid] == target) {
                    return mid;
                } else if (A[left] < A[mid]) {
                // remember to pay attention to (A[left] == target) case
                    if (A[left] <= target && target < A[mid]) {
                        right = mid;
                    } else {
                        left = mid;
                    }
                } else {
                // remember to pay attention to (A[right] == target) case
                    if (A[mid] < target && target <= A[right]) {
                        left = mid;
                    } else {
                        right = mid;
                    }
                }
            }
            if (A[left] == target) {
                return left;
            } else if (A[right] == target) {
                return right;
            }
            return -1;
        }
    }
