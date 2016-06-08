---
layout: post
title: "[LeetCode 74] Search a 2D Matrix"
comments: true
category: Leetcode

---

### Question 

[link](https://oj.leetcode.com/problems/search-a-2d-matrix/)

<div class="question-content">
            <p></p><p>Write an efficient algorithm that searches for a value in an <i>m</i> x <i>n</i> matrix. This matrix has the following properties:</p>

<p>
</p><ul>
<li>Integers in each row are sorted from left to right.</li>
<li>The first integer of each row is greater than the last integer of the previous row.</li>
</ul>
<p></p>

<p>
For example,</p>
<p>
Consider the following matrix:
</p>
<pre>[
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
</pre>

<p>Given <b>target</b> = <code>3</code>, return <code>true</code>.</p><p></p>
          </div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
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
		<td bgcolor="red">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Related questions

__[Search a 2D Matrix]({% post_url /leetcode/2014-05-21-Search-a-2D-Matrix %})__. 

__[Searching a 2D Sorted Matrix]({% post_url /leetcode_plus/2014-06-10-Searching-a-2D-Sorted-Matrix %})__. 

__[Count negative in a 2D Sorted Matrix]({% post_url /question/2014-06-14-Count-negative-in-2D-Sorted-Matrix %})__. 

### Analysis

__This is a binary search question__. 

### Solution

I did not use binary, but use the easier linear search. It still passed. 

### Code

__my code revised (2D binary search)__

    public boolean searchMatrix(int[][] matrix, int target) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return false;
        }
        int m = matrix.length;
        int n = matrix[0].length;
        // find target vertically from matrix[0] to matrix[m-1]
        int top = 0, bottom = m - 1;
        int mid;
        while (top + 1 < bottom) {
            mid = top + (bottom - top) / 2;
            if (matrix[mid][0] < target) {
                top = mid;
            }
            else {
                bottom = mid;
            }
        }
        // locate the row number
        int row = -1;
        if (matrix[top][0] <= target && target <= matrix[top][n-1]) {
            row = top;
        }
        else if (matrix[bottom][0] <= target && target <= matrix[bottom][n-1]) {
            row = bottom;
        }
        else {
            return false;
        }
        // now find target from matrix[row]
        int left = 0, right = n - 1;
        while (left + 1 < right) {
            mid = left + (right - left) / 2;
            if (matrix[row][mid] < target) {
                left = mid;
            }
            else {
                right = mid;
            }
        }
        return (matrix[row][left] == target || matrix[row][right] == target);
    }

__A good binary search code [here](http://www.programcreek.com/2013/01/leetcode-search-a-2d-matrix-java/) (1D binary search)__


    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix==null || matrix.length==0 || matrix[0].length==0) 
            return false;

        int m = matrix.length;
        int n = matrix[0].length;
        int start = 0;
        int end = m*n-1;

        while(start<=end){
            int mid=(start+end)/2;
            int midX=mid/n;
            int midY=mid%n;

            if(matrix[midX][midY]==target) 
                return true;
            if(matrix[midX][midY]<target){
                start=mid+1;
            }else{
                end=mid-1;
            }
        }
        return false;
    }
