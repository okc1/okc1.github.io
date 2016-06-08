---
layout: post
title: "[LeetCode 63] Unique Paths II"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/unique-paths-ii/)

<div class="question-content">
            <p></p><p>Follow up for "Unique Paths":</p>

<p>Now consider if some obstacles are added to the grids. How many unique paths would there be?</p>

<p>An obstacle and empty space is marked as <code>1</code> and <code>0</code> respectively in the grid.</p>

<p>For example,<br>
</p><p>There is one obstacle in the middle of a 3x3 grid as illustrated below.</p>
<pre>[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
</pre>
<p>The total number of unique paths is <code>2</code>.</p>

<p><b>Note:</b> <i>m</i> and <i>n</i> will be at most 100.</p><p></p>
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
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Solution

__This is similar question as previous one, but DP solution__. 

### My code

	public class Solution {
	    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
	        int[][] ob = obstacleGrid;
	        if (ob == null || ob.length == 0) {
	            return 0;
	        }
	        int m = ob.length;
	        int n = ob[0].length;
	        int[][] dp = new int[m][n];
	        for (int i = 0; i < m; i++) {
	            for (int j = 0; j < n; j++) {
	                if (i == 0 && j == 0) {
	                    dp[i][j] = ob[i][j] == 1 ? 0 : 1;
	                } else if (i == 0) {
	                    dp[i][j] = dp[i][j - 1] * (ob[i][j] == 1 ? 0 : 1);
	                } else if (j == 0) {
	                    dp[i][j] = dp[i - 1][j] * (ob[i][j] == 1 ? 0 : 1);
	                } else {
	                    if (ob[i][j] == 1) {
	                        dp[i][j] = 0;
	                    } else {
	                        dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
	                    }
	                }
	            }
	        }
	        return dp[m - 1][n - 1];
	    }
	}
