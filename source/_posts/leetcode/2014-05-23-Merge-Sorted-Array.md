---
layout: post
title: "[LeetCode 88] Merge Sorted Array"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/merge-sorted-array/)

<div class="question-content">
            <p></p><p>Given two sorted integer arrays A and B, merge B into A as one sorted array.</p>

<p>
<b>Note:</b><br>
You may assume that A has enough space (size that is greater or equal to <i>m</i> + <i>n</i>) to hold additional elements from B. The number of elements initialized in A and B are <i>m</i> and <i>n</i> respectively.</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is an easy question.__

### Solution

Just insert from the end to the head. 

### Code

    public void merge(int A[], int m, int B[], int n) {
        int p1 = m - 1, p2 = n - 1;
        for (int i = m + n - 1; i >= 0; i --){
            if (p2 == -1) return;
            if (p1 == -1) {
                for (int j = 0; j <= p2; j++) A[j] = B[j];
                return;
            }
            if (A[p1] > B[p2]) A[i] = A[p1--];
            else A[i] = B[p2--];
        }
    }