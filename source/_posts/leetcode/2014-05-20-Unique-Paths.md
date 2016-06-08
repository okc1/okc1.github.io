---
layout: post
title: "[LeetCode 62] Unique Paths"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/unique-paths/)

<div class="question-content">
            <p></p><p>A robot is located at the top-left corner of a <i>m</i> x <i>n</i> grid (marked 'Start' in the diagram below).</p>

<p>The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).</p>

<p>How many possible unique paths are there?</p>

<p>
<img src="http://4.bp.blogspot.com/_UElib2WLeDE/TNJf8VtC2VI/AAAAAAAACXU/UyUa-9LKp4E/s400/robot_maze.png"><br>
</p><p style="font-size: 11px">Above is a 3 x 7 grid. How many possible unique paths are there?
</p>

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
		<td bgcolor="lime">2</td>
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

__This is an easy question__.

Basically to walk from (0,0) to (m,n), robot have to walk down (m-1) steps and rightward (n-1) steps. Then this problem simply becomes [Number of k-combinations](http://en.wikipedia.org/wiki/Combination#Number_of_k-combinations) (also known as choose m from n problem). The code is just concise and short. 

### My code

	public class Solution {
	    public int uniquePaths(int m, int n) {
	        m--;
	        n--;
	        if (m < 0 || n < 0) {
	            return 0;
	        } else if (m == 0 || n == 0) {
	            return 1;
	        }
	        long sum = 1;
	        // the answer would be "choose m from (m + n)"
	        if (m > n) {
	            int temp = m;
	            m = n;
	            n = temp;
	        }
	        int num = m + n;
	        for (int i = 0; i < m; i++) {
	            sum *= (num - i);
	        }
	        for (int i = 0; i < m; i++) {
	            sum /= (i + 1);
	        }
	        return (int) sum;
	    }
	}
