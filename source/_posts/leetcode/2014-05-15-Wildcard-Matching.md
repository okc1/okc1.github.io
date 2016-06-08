---
layout: post
title: "[LeetCode 44] Wildcard Matching"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/wildcard-matching/)

<div class="question-content">
            <p></p><p>Implement wildcard pattern matching with support for <code>'?'</code> and <code>'*'</code>.</p>

<pre>'?' Matches any single character.
'*' Matches any sequence of characters (including the empty sequence).

The matching should cover the <b>entire</b> input string (not partial).

The function prototype should be:
bool isMatch(const char *s, const char *p)

Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "*") → true
isMatch("aa", "a*") → true
isMatch("ab", "?*") → true
isMatch("aab", "c*a*b") → false
</pre><p></p>
          </div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

This question is similar to "Regex Matching", and in fact can be solved using similar (DFS recursion) approach. [This blog](http://n00tc0d3r.blogspot.sg/2013/05/wildcard-matching.html) has the best analysis and solutions.

__The solution is DP__. The equation is not very difficult to write, but keep in mind to __check character count before entering the algorithm__. Failing to do so results in TLE. 

### My code 

	public class Solution {
	    public boolean isMatch(String s, String p) {
	        if (s == null || p == null) {
	            return true;
	        }
	        
	        // pre-check
	        int count = 0;
	        for (int i = 0; i < p.length(); i++) {
	            if (p.charAt(i)!='*') count++;
	        }
	        if(count > s.length()) {
	            return false;  
	        }
	        // end of pre-check
	        
	        int m = s.length();
	        int n = p.length();
	        // note the order is n,m, 
	        // cuz we match each chars of p with chars of s
	        boolean[][] dp = new boolean[n + 1][m + 1];
	        for (int i = 0; i <= n; i++) {
	            for (int j = 0; j <= m; j++) {
	                if (i == 0 && j == 0) {
	                    dp[i][j] = true;
	                } else if (i == 0) {
	                    dp[i][j] = false;
	                } else if (j == 0) {
	                    // there is a special case: ("", "*")
	                    if (p.charAt(i - 1) == '*' && dp[i-1][j]) {
	                        dp[i][j] = true;
	                    } else {
	                        dp[i][j] = false;
	                    }
	                } else if (p.charAt(i - 1) != '*') {
	                    if (dp[i-1][j-1]) {
	                        if (p.charAt(i - 1) == '?' || p.charAt(i - 1) == s.charAt(j - 1)) {
	                            // single char matches
	                            dp[i][j] = true;
	                        }
	                    }
	                } else {
	                    // current char from p is a star
	                    // find the first place at which p matches with s
	                    int pos = 0;
	                    while (pos <= m && !dp[i-1][pos]) {
	                        pos++;
	                    }
	                    // starting from pos, all subsequent substring of s matches p
	                    while (pos <= m) {
	                        dp[i][pos++] = true;
	                    }
	                    // important to break the for loop here and do not check for row i any more
	                    // this requires changing the nested loop to put j outside of i
	                    // the execution time decrease from TLE/1800ms to 800ms by adding this line
	                    break;
	                    // this break finished off all check for row i, and i advance to next row
	                }
	            }
	        }
	        return dp[n][m];
	    }
	}
