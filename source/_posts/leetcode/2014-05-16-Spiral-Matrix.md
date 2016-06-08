---
layout: post
title: "[LeetCode 54] Spiral Matrix"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/spiral-matrix/)

<div class="question-content">
            <p></p><p>Given a matrix of <i>m</i> x <i>n</i> elements (<i>m</i> rows, <i>n</i> columns), return all elements of the matrix in spiral order.
</p>

<p>
For example,<br>
Given the following matrix:
</p>
<pre>[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
</pre>
<p>
You should return <code>[1,2,3,6,9,8,7,4,5]</code>.
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
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This question is basic mathematics__. The difficulty is the coding part. 

### My code

	public class Solution {
	    public List<Integer> spiralOrder(int[][] matrix) {
			List<Integer> ans = new ArrayList<Integer>();
			if (matrix == null || matrix.length == 0 
				|| matrix[0] == null || matrix[0].length == 0) {
				return ans;
			}
			int m = matrix.length;
			int n = matrix[0].length;
			int a = 0;
			int b = 0;
			while (a < (m + 1) / 2 && b < (n + 1) / 2) {
				// special cases
				if (2 * a + 1 == m && 2 * b + 1 == n) {
					ans.add(matrix[a][b]);
					break;
				} else if (2 * a + 1 == m) {
					for (int j = b; j <= n - 1 - b; j++) {
						ans.add(matrix[a][j]);
					}
					break;
				} else if (2 * b + 1 == n) {
					for (int i = a; i <= m - 1 - a; i++) {
						ans.add(matrix[i][b]);
					}
					break;
				}
				// now is the general case
				// first horizontal row without last element
				for (int j = b; j < n - 1 - b; j++) {
					ans.add(matrix[a][j]);
				}
				// vertical column on right-hand side
				for (int i = a; i < m - 1 - a; i++) {
					ans.add(matrix[i][n - 1 - b]);
				}
				for (int j = n - 1 - b; j > b; j--) {
					ans.add(matrix[m - 1 - a][j]);
				}
				for (int i = m - 1 - a; i > a; i--) {
					ans.add(matrix[i][b]);
				}
				a++;
				b++;
			}
			return ans;
	    }
	}
