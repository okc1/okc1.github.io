---
layout: post
title: "[LeetCode 48] Rotate Image"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/rotate-image/)

<div class="question-content">
            <p></p><p>You are given an <i>n</i> x <i>n</i> 2D matrix representing an image.</p>
<p>Rotate the image by 90 degrees (clockwise).</p>
<p>Follow up:<br>
Could you do this in-place?</p><p></p>
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
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Solution

This question is easy, just swap numbers in place. 

### My code 

    public class Solution {
        public void rotate(int[][] matrix) {
            if (matrix == null) {
                return;
            }
            int N = matrix.length;
            // 5 - 2/3
            // 6 - 3/3
            int m = N / 2;
            int n = (N + 1) / 2;
            for (int i = 0; i < m; i++) {
                for (int j = 0; j < n; j++) {
                    // eg. N = 4, i = 0, j = 1
                    // (0, 1) <- (2, 0)
                    // (2, 0) <- (3, 2)
                    // (3, 2) <- (1, 3)
                    // (1, 3) <- (0, 1)
                    int temp = matrix[i][j];
                    matrix[i][j] = matrix[N - 1 - j][i];
                    matrix[N - 1 - j][i] = matrix[N - 1 - i][N - 1 - j];
                    matrix[N - 1 - i][N - 1 - j] = matrix[j][N - 1 - i];
                    matrix[j][N - 1 - i] = temp;
                }
            }
        }
    }

A cleaner version from [this blog](http://blog.csdn.net/kenden23/article/details/17200067). 

This code is very concise and beautiful, because it __added the following 2 variables__: 

> x = n-1-a
>
> y = n-1-b

    public void rotate(int[][] matrix) {
        for (int a = 0, x = matrix.length - 1; a < x; a++, x--) {
            for (int b = a, y = x; b < x; b++, y--) {
                int t = matrix[a][b];
                matrix[a][b] = matrix[y][a];
                matrix[y][a] = matrix[x][y];
                matrix[x][y] = matrix[b][x];
                matrix[b][x] = t;
            }
        }
    }
