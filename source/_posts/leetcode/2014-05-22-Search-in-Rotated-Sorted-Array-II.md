---
layout: post
title: "[LeetCode 81] Search in Rotated Sorted Array II"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/search-in-rotated-sorted-array-ii/)

<div class="question-content">
            <p></p><p>Follow up for "Search in Rotated Sorted Array":<br>
What if <i>duplicates</i> are allowed?</p>

<p>Would this affect the run-time complexity? How and why?</p>

<p>Write a function to determine if a given target is in the array.</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This one is based on the solution of previous question__. 

The previous question is already very difficult, both the logic and coding part. However, if you solve previous question by yourself, you will do this one easily. 

I will pick the 2nd piece of code in previous question, and modify it to solve this problem. 

> Solution for previous question:


    public int search(int[] A, int target) {
        int left = 0;
        int right = A.length - 1;
        while (left <= right) {
            int mid = (left + right) / 2;
            if (target == A[mid]) return mid;
            if (A[left] <= A[mid]) {
                if (A[left] <= target && target <= A[mid]) right = mid;
                else left = mid + 1;
            } else {
                if (A[mid] <= target && target <= A[right]) left = mid;
                else right = mid - 1;
            }
        }
        return -1;
    }


### Solution

__My solution is to skip all duplicated numbers__ before the while-loop. 

__The most standard solution is left-pointer incremental__. A good code is written from [this blog](http://www.cnblogs.com/feiling/p/3231196.html).

### Code

__First, my solution__

    public boolean search(int[] A, int target) {
        int len = A.length, L = 0, R = len - 1;
        if (A[L] == A[R]) {
            int duplicate = A[R];
            if (duplicate == target) return true;
            while (L < len && A[L] == duplicate) L ++;
            while (R >= 0 && A[R] == duplicate) R --;
        }
        while (L <= R) {
            // Avoid overflow, same as M=(L+R)/2
            int M = L + ((R - L) / 2);
            if (A[M] == target) return true;
            // the bottom half is sorted
            if (A[L] <= A[M])
                if (A[L] <= target && target < A[M]) R = M - 1;
                else L = M + 1;
            // the upper half is sorted
            else 
                if (A[M] < target && target <= A[R]) L = M + 1;
                else R = M - 1;
        }
        return false;
    }

__Second, standard solution__

    public boolean search(int[] A, int target) {
        int len = A.length, L = 0, R = len - 1;
        while (L <= R) {
            int M = L + ((R - L) / 2);
            if (A[M] == target) return true;
            if (A[L] < A[M])
                if (A[L] <= target && target < A[M]) R = M - 1;
                else L = M + 1;
            else if (A[L] > A[M])
                if (A[M] < target && target <= A[R]) L = M + 1;
                else R = M - 1;
            else L ++;
        }
        return false;
    }