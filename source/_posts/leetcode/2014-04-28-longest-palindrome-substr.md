---
layout: post
title: "[LeetCode 5] Longest Palindromic Substring "
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/longest-palindromic-substring/)

<div class="question-content">
<p></p><p>Given a string <i>S</i>, find the longest palindromic substring in <i>S</i>. You may assume that the maximum length of <i>S</i> is 1000, and there exists one unique longest palindromic substring.</p><p></p>
</div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

There are 2 solutions. One is __DP__ which is O(N^2) time and O(N^2) space. Another is "Search around corner", which uses less space. 

### Solution

__DP solution is straight-forward__. Use 2D array to check palindrome intervals and make it as either true or false. Meanwhile, update longest. 

O(N^2) time and O(N^2) space

__Search around corner__ is basically iterate through the entire string and assume each char (or char pair) as center of the palindrome. The code isn't difficult once you come up with the idea. 

For more, read [this post](http://leetcode.com/2011/11/longest-palindromic-substring-part-i.html)

O(N^2) time and O(1) space

### My code 

DP solution

    public class Solution {
        public String longestPalindrome(String s) {
            if (s == null || s.length() == 0) {
                return "";
            }
            String longest = "";
            int len = s.length();
            // dp[i][j] means substring of s from i to j is palindrome 
            boolean[][] dp = new boolean[len][len];
            // why i decrease from (len-1) to 0, but j increase from i to (len-1)?
            // think about it! 
            for (int i = len - 1; i >= 0; i--) {
                for (int j = i; j < len; j++) {
                    if (i == j) {
                        dp[i][j] = true;
                    } else if (i + 1 == j) {
                        dp[i][j] = s.charAt(i) == s.charAt(j);
                    } else {
                        // important to note: dp[i+1][j-1]
                        // i depends on (i+1), so i from large to small
                        // j is just the opposite, small to large
                        dp[i][j] = s.charAt(i) == s.charAt(j) && dp[i+1][j-1];
                    }
                    if (dp[i][j] && j + 1 - i > longest.length()) {
                        longest = s.substring(i, j + 1);
                    }
                }
            }
            return longest;
        }
    }

Search around corner

    public class Solution {
        public String longestPalindrome(String s) {
            if (s.length() <= 1)
                return s;
            String largest = s.substring(0, 1);
            for (int i = 0; i < s.length(); i++) {
                String first = this.searchAroundCenter(s, i, i);
                String second = this.searchAroundCenter(s, i, i + 1);
                if (first.length() < second.length())
                    first = second;
                if (largest.length() < first.length())
                    largest = first;
            }
            return largest;
        }

        private String searchAroundCenter(String s, int a, int b) {
            if (a < 0 || b > s.length() - 1)
                return "";
            while (s.charAt(a) == s.charAt(b)) {
                a--;
                b++;
                if (a < 0 || b > s.length() - 1)
                    return s.substring(a + 1, b);
            }
            return s.substring(a + 1, b);
        }
    }
