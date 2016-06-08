---
layout: post
title: "[LeetCode 97] Interleaving String"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/interleaving-string/)

<div class="question-content">
            <p></p><p>
Given <i>s1</i>, <i>s2</i>, <i>s3</i>, find whether <i>s3</i> is formed by the interleaving of <i>s1</i> and <i>s2</i>.
</p>

<p>
For example,<br>
Given:<br>
<i>s1</i> = <code>"aabcc"</code>,<br>
<i>s2</i> = <code>"dbbca"</code>,
</p>
<p>
When <i>s3</i> = <code>"aadbbcbcac"</code>, return true.<br>
When <i>s3</i> = <code>"aadbbbaccc"</code>, return false.
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
		<td bgcolor="red">5</td>
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

__This is a DP question__.

At first look it might look like very easily solved by DFS. It it, but TLE exception. 

So, I learnt the idea from [this blog](http://blog.csdn.net/u011095253/article/details/9248073). It's easy to realize this is a __very standard DP question__. 

### Solution

Declare a 2-D array for DP, and dp(i)(j) denotes whether it's possible to construct s3 (of length i+j) by using s1 (of length i) and s2 (of length j). 

Only thing needs to mention is the size of dp is (m+1)*(n+1), because i = \[0, m\] and j = \[0, n\]. 

### Code

__DP solution__

    public boolean isInterleave(String s1, String s2, String s3) {
        int len1 = s1.length();
        int len2 = s2.length();
        int len3 = s3.length();
        if (len1 + len2 != len3) return false;
        boolean[][] dp = new boolean[len1 + 1][len2 + 1];
        dp[0][0] = true;
        for (int i = 1; i <= len2; i ++)
            dp[0][i] = dp[0][i - 1] & s2.charAt(i-1) == s3.charAt(i-1);
        for (int i = 1; i <= len1; i ++)
            dp[i][0] = dp[i-1][0] & s1.charAt(i-1) == s3.charAt(i-1);
        for (int i = 1; i <= len1; i ++) {
            for (int j = 1; j <= len2; j ++) {
                if (s1.charAt(i-1) == s3.charAt(i+j-1) && dp[i-1][j])
                    dp[i][j] = true;
                if (s2.charAt(j-1) == s3.charAt(i+j-1) && dp[i][j-1])
                    dp[i][j] = true;
            }
        }
        return dp[len1][len2];
    }
