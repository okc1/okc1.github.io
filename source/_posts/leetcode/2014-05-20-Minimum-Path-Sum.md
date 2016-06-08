---
layout: post
title: "[LeetCode 64] Minimum Path Sum"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/minimum-path-sum/)

<div class="question-content">
            <p></p><p>Given a <i>m</i> x <i>n</i> grid filled with non-negative numbers, find a path from top left to bottom right which <i>minimizes</i> the sum of all numbers along its path.</p>

<p><b>Note:</b> You can only move either down or right at any point in time.</p><p></p>
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

### Analysis

__This is a very easy DP problem__. 

But this is not a boring question because I found a few interesting solutions. 

### Solution

__Code 1 is 2-D DP__. 

__2nd code is from [this blog](http://fisherlei.blogspot.sg/2012/12/leetcode-minimum-path-sum.html)__. Instead of 2-D array, it simply uses a "rotational array" (滚动数组), or 1-D array. 

__3rd code is using no extra space__. It works in place.

### My code

__2D array__

	public class Solution {
	    public int minPathSum(int[][] grid) {
	        if (grid == null || grid.length == 0) {
	            return 0;
	        }
	        int m = grid.length;
	        int n = grid[0].length;
	        int[][] dp = new int[m][n];
	        for (int i = 0; i < m; i++) {
	            for (int j = 0; j < n; j++) {
	                if (i == 0 && j == 0) {
	                    dp[i][j] = grid[i][j];
	                } else if (i == 0) {
	                    dp[i][j] = grid[i][j] + dp[i][j - 1];
	                } else if (j == 0) {
	                    dp[i][j] = grid[i][j] + dp[i - 1][j];
	                } else {
	                    dp[i][j] = grid[i][j] + Math.min(dp[i - 1][j], dp[i][j - 1]);
	                }
	            }
	        }
	        return dp[m - 1][n - 1];
	    }
	}


__1-D array__


    public int minPathSum(int[][] grid) {
        if (grid.length == 0) return 0;
        if (grid[0].length == 0) return 0;
        int[] dp = new int[grid[0].length];
        for (int i = 0; i < grid.length; i ++) 
            for (int j = 0; j < grid[0].length; j ++) 
                if (i == 0 && j == 0) dp[j] = grid[0][0];
                else if (i == 0) dp[j] = dp[j-1] + grid[i][j];
                else if (j == 0) dp[j] += grid[i][j];
                else dp[j] = Math.min(dp[j-1], dp[j]) + grid[i][j];
        return dp[dp.length-1];
    }

__in-place__

    public int minPathSum(int[][] grid) {
        if (grid.length == 0) return 0;
        if (grid[0].length == 0) return 0;
        for (int i = 0; i < grid.length; i ++) 
            for (int j = 0; j < grid[0].length; j ++) 
                if (i == 0 && j == 0) continue;
                else if (i == 0) grid[i][j] = grid[i][j] + grid[i][j-1];
                else if (j == 0) grid[i][j] = grid[i][j] + grid[i-1][j];
                else grid[i][j] = Math.min(grid[i-1][j], grid[i][j-1]) + grid[i][j];
        return grid[grid.length-1][grid[0].length-1];
    }
