---
layout: post
title: "[LeetCode 75] Sort Colors"
comments: true
category: Leetcode

---

### Question 
[link](https://oj.leetcode.com/problems/sort-colors/)

<div class="question-content">
            <p></p><p>
Given an array with <i>n</i> objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.
</p>

<p>
Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.
</p>

<p>
<b>Note:</b><br>
You are not suppose to use the library's sort function for this problem.
</p>

<div class="spoilers" >
<p><b>Follow up:</b><br>
A rather straight forward solution is a two-pass algorithm using counting sort.<br>
First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's.</p>
<p>Could you come up with an one-pass algorithm using only constant space?<br>
</p>
</div><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="lime">2</td>
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
		<td bgcolor="yellow">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a extremely interesting question, with very tricky solutions__. But the 3rd piece of code is actually the standard solution (by making use of the idea from __partition array__). 

### Code

__First solution came from__ [this blog](https://oj.leetcode.com/discuss/1827/anyone-with-one-pass-and-constant-space-solution).


    public void sortColors(int[] A) {
        int a = -1, b = -1, c = -1;
        for (int i = 0; i < A.length; i ++) {
            if (A[i] == 0) {
                A[++ c] = 2;
                A[++ b] = 1;
                A[++ a] = 0;
            } else if (A[i] == 1) {
                A[++ c] = 2;
                A[++ b] = 1;
            } else {
                A[++ c] = 2;
            }
        }
    }

__Second solution, 2 pointer & swap__ which is written [here](http://fisherlei.blogspot.sg/2013/01/leetcode-sort-colors.html). 

    public void sortColors(int[] A) {
        int len = A.length;
        int i = 0, x = 0, y = len - 1;
        while (i <= y) {
            if (A[i] == 0) 
                swap(A, i ++, x ++);
            else if (A[i] == 2) 
                swap(A, i, y --);
            else i ++;
        }
    }

    private void swap(int[] A, int a, int b) {
        int temp = A[a];
        A[a] = A[b];
        A[b] = temp;
    }

__Updated on July 4th, 2014__: Use of solution of __Partition Array__ to partition colors twice: 

1. first time move all 0 to left.
1. second time move all 1 to left, following the 0s. 

Code :

    public void sortColors(int[] A) {
        if (A == null || A.length == 0) {
			return;
		}
		int len = A.length;
		partition(A, 0, len - 1, 0);
		int p = 0;
		while (p < len && A[p] == 0) {
			p++;
		}
		partition(A, p, len - 1, 1);
    }
	
	private void partition(int[] A, int start, int end, int target) {
		// find the target and put it on the left side of the array
		while (start < end) {
			while (start < A.length && A[start] == target) {
				start++;
			}
			while (end >= 0 && A[end] != target) {
				end--;
			}
			if (start > end) {
				break;
			} else {
				int temp = A[start];
				A[start] = A[end];
				A[end] = temp;
			}
		}
	}
