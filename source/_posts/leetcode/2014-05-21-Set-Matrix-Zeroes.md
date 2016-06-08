---
layout: post
title: "[LeetCode 73] Set Matrix Zeroes"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/set-matrix-zeroes/)

<div class="question-content">
            <p></p><p>
Given a <i>m</i> x <i>n</i> matrix, if an element is 0, set its entire row and column to 0. Do it in place.
</p>

<div class="spoilers"><b>Follow up:</b>

<p>
Did you use extra space?<br>
A straight forward solution using O(<i>m</i><i>n</i>) space is probably a bad idea.<br>
A simple improvement uses O(<i>m</i> + <i>n</i>) space, but still not the best solution.<br>
Could you devise a constant space solution?
</p>
</div><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
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

__This is a very borning question__. The O(m+n) space solution is trivial, I will not cover. The constant space solution is __making use of 1st row and 1st columns__ of the input array. 

### Solution

__The idea is clear enough__, but writing the code is not as easy. [This post](http://www.programcreek.com/2012/12/leetcode-set-matrix-zeroes-java/) is a good explanation and code for the solution. 

__Difficult point__: when there's 0, set 0; but when there is no 0, do not touch on the value (if original it's 3, keep it 3). 

### Code


    public void setZeroes(int[][] matrix) {
        int m = matrix.length;
        if (m == 0) return;
        int n = matrix[0].length;
        if (n == 0) return;

        int firstrow = 1, firstcol = 1;
        for (int i = 0; i < m; i ++) 
            if (matrix[i][0] == 0) 
                firstcol = 0;
        for (int i = 0; i < n; i ++) 
            if (matrix[0][i] == 0) 
                firstrow = 0;
        for (int i = 1; i < m; i ++) {
            for (int j = 1; j < n; j ++) {
                if (matrix[i][j] == 0) {
                    matrix[i][0] = 0;
                    matrix[0][j] = 0;
                }
            }
        }
        for (int i = 1; i < m; i ++) {
            if (matrix[i][0] == 0)
                for (int j = 1; j < n; j ++) 
                    matrix[i][j] = 0;
            if (firstcol == 0) matrix[i][0] = 0;
        }
        for (int i = 1; i < n; i ++) {
            if (matrix[0][i] == 0)
                for (int j = 1; j < m; j ++) 
                    matrix[j][i] = 0;
            if (firstrow == 0) matrix[0][i] = 0;
        }
        if(firstrow == 0 || firstcol == 0) 
            matrix[0][0] = 0;
    }
