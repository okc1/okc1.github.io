---
layout: post
title: "[LeetCode 115] Distinct Subsequences"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/distinct-subsequences/)

<div class="question-content">
            <p></p><p>
Given a string <b>S</b> and a string <b>T</b>, count the number of distinct subsequences of <b>T</b> in <b>S</b>.
</p>

<p>
A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, <code>"ACE"</code> is a subsequence of <code>"ABCDE"</code> while <code>"AEC"</code> is not).
</p>

<p>
Here is an example:<br>
<b>S</b> = <code>"rabbbit"</code>, <b>T</b> = <code>"rabbit"</code>
</p>
<p>
Return <code>3</code>.
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
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is an extremely difficult DP question__, probably the most difficult DP on leetcode. 

Normally, string matching question is best solved with DP, so is this question. The problem is how to construct the __[Bellman equation](http://en.wikipedia.org/wiki/Bellman_equation)__ (also known as dynamic programming equation). 

__Updated on June 24th__, I listed down one example using S = "abab" and T = "ab". 

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg .tg-s6z2{text-align:center}
</style>
<table class="tg">
  <tr>
    <th class="tg-s6z2"></th>
    <th class="tg-031e">{}</th>
    <th class="tg-031e">a</th>
    <th class="tg-031e">b</th>
  </tr>
  <tr>
    <td class="tg-031e">{}</td>
    <td class="tg-031e">1</td>
    <td class="tg-031e">0</td>
    <td class="tg-031e">0</td>
  </tr>
  <tr>
    <td class="tg-031e">a</td>
    <td class="tg-031e">1</td>
    <td class="tg-031e">1</td>
    <td class="tg-031e">0</td>
  </tr>
  <tr>
    <td class="tg-031e">b</td>
    <td class="tg-031e">1</td>
    <td class="tg-031e">1</td>
    <td class="tg-031e">1</td>
  </tr>
  <tr>
    <td class="tg-031e">a</td>
    <td class="tg-031e">1</td>
    <td class="tg-031e">2</td>
    <td class="tg-031e">1</td>
  </tr>
  <tr>
    <td class="tg-031e">b</td>
    <td class="tg-031e">1</td>
    <td class="tg-031e">2</td>
    <td class="tg-031e">3</td>
  </tr>
</table>

### Solution

It took me a really long time to understand, until I read [this blog](http://www.programcreek.com/2013/01/leetcode-distinct-subsequences-total-java/). 

> Let W(i, j) stand for the number of subsequences of S(0, i) in T(0, j). If S.charAt(i) == T.charAt(j), W(i, j) = W(i-1, j-1) + W(i-1,j); Otherwise, W(i, j) = W(i-1,j).

Two code are posted below, realizing this solution with 2D and 1D array respectively (first code is better). 

### Code

__First, DP code__

    public int numDistinct(String S, String T) {
		int m = S.length(), n = T.length();
        int[][] dp = new int[m + 1][n + 1];
		for (int i = 0; i <= m; i ++) {
			for (int j = 0; j <= n; j ++) {
				if (j == 0) dp[i][j] = 1;
				else if (i == 0) dp[i][j] = 0;
				else if (S.charAt(i-1) == T.charAt(j-1)) 
					dp[i][j] = dp[i-1][j-1] + dp[i-1][j];
				else
					dp[i][j] = dp[i-1][j];
			}
		}
		return dp[m][n];
    }

__Second, same solution but reduced 2-D array to 1-D__.

Code readability is reduced, however.

    public int numDistinct(String S, String T) {
		int m = S.length(), n = T.length();
        int[] dp = new int[n + 1];
		for (int i = 0; i <= m; i ++) {
			for (int j = n; j >= 0; j --) {
				if (j == 0) 
					dp[j] = 1;
				else if (i == 0) 
					dp[j] = 0;
				else if (S.charAt(i-1) == T.charAt(j-1)) 
					dp[j] = dp[j-1] + dp[j];
			}
		}
		return dp[n];
    }
