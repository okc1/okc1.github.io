---
layout: post
title: "[LeetCode 52] N-Queens II"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/n-queens-ii/)

<div class="question-content">
            <p></p><p>Follow up for N-Queens problem.</p>

<p>Now, instead outputting board configurations, return the total number of distinct solutions.</p>

<p><img src="http://www.leetcode.com/wp-content/uploads/2012/03/8-queens.png"></p><p></p>
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
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Solution

I posted 2 solution by me. Second code is same as [this guy's code](https://github.com/rffffffff007/leetcode/blob/master/N-Queens%20II.java).

### My code

__Using global variable__ (similar to [LeetCode 51] N-Queens)

	public class Solution {
	    
	    int total = 0;
	    
	    public int totalNQueens(int n) {
	        if (n <= 0) {
	            return 0;
	        }
	        int[] map = new int[n];
	        helper(map, 0, n);
	        return total;
	    }
	    
	    private void helper(int[] map, int row, int n) {
	        if (row == n) {
	            total++;
	            return;
	        }
	        for (int i = 0; i < n; i++) {
	            map[row] = i;
	            // check if map[row] conflicts with any row above
	            boolean valid = true;
	            for (int k = 0; k < row; k++) {
	                if (Math.abs(map[k] - map[row]) == row - k || map[k] == map[row]) {
	                    // not valid!
	                    valid = false;
	                    break;
	                }
	            }
	            if (valid) {
	                helper(map, row + 1, n);
	            }
	        }
	    }
	}

__Without using global variable__

	public class Solution {
	    public int totalNQueens(int n) {
	        return solve(0, n, new int[n]);
	    }
	
	    private int solve(int cur, int n, int[] list) {
	        if (cur == n) return 1;
	        int ans = 0;
	        for (int i = 0; i < n; i++) {
	            boolean conflict = false;
	            for (int j = 0; j < cur; j++)
	                if (i == list[j] || cur - j == Math.abs(i - list[j]))
	                    conflict = true;
	            if (conflict) continue;
	            list[cur] = i;
	            ans += solve(cur + 1, n, list);
	        }
	        return ans;
	    }
	}
