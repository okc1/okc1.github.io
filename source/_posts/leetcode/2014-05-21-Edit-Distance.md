---
layout: post
title: "[LeetCode 72] Edit Distance"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/edit-distance/)

<div class="question-content">
            <p></p><p>
Given two words <i>word1</i> and <i>word2</i>, find the minimum number of steps required to convert <i>word1</i> to <i>word2</i>. (each operation is counted as 1 step.)
</p>

<p>
You have the following 3 operations permitted on a word:
</p>

<p>
a) Insert a character<br>
b) Delete a character<br>
c) Replace a character<br>
</p><p></p>
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
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a difficult DP problem__. A lot of people said in their blog that they spent tons of time on this question. 

### Solution

__I posted below a very standard solution__. The unconventional part of this solution is instead of declaring DP array of m\*n size, I must declare it (m+1)\*(n+1) size, where dp\[i\]\[j\] denotes the distance of 2 strings that ends with (i)th and (j)th char respectively. 

The rest of the code is easy to understand. 

### Code

__my code__


    public int minDistance(String word1, String word2) {
        int m = word1.length();
        int n = word2.length();

        int[][] dp = new int[m+1][n+1];
        for (int i = 0; i <= m; i++) {
            dp[i][0] = i;
        }
        for (int i = 0; i <= n; i++) {
            dp[0][i] = i;
        }
        for (int a = 1; a <= m; a++) {
            char aa = word1.charAt(a-1);
            for (int b = 1; b <= n; b++) {
                char bb = word2.charAt(b-1);
                if (aa == bb) 
                    dp[a][b] = dp[a-1][b-1];
                else {
                    int t1 = dp[a-1][b-1] + 1;
                    int t2 = dp[a][b-1] + 1;
                    int t3 = dp[a-1][b] + 1;
                    dp[a][b] = Math.min(Math.min(t1, t2), t3);
                }
            }
        }
        return dp[m][n];
    }
