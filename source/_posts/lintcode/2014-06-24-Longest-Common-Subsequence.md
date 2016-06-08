---
layout: post
title: "[LintCode] Longest Common Subsequence"
comments: true
category: LintCode

---

### Question 

[link](http://lintcode.com/en/problem/longest-common-subsequence/)

<div style="min-height:100px">
    <p>Given two strings, find the longest comment subsequence (LCS).</p>
    <p>Your code should return the length of LCS.</p>
    <div class="m-t-lg m-b-lg">
    <b>Example</b>
    <div>
        <p>For "ABCD" and "EDCA", the LCS is "A" (or D or C), return 1</p>
        <p>For "ABCD" and "EACB", the LCS is "AC", return 2</p>
    </div>
    </div>
</div>

### Analysis 

This is one of the __2 most popular questions of DP__. 

This is a two-sequences Dp. The equation is not difficult to build. (consider only the last element of the DP array when building the state transition equation)

### Code

    public int longestCommonSubsequence(String A, String B) {
        // write your code here
        if (A == null || B == null) {
            return 0;
        }
        int m = A.length(), n = B.length();
        int[][] dp = new int[m + 1][n + 1];
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (A.charAt(i - 1) == B.charAt(j - 1)) {
                    dp[i][j] = 1 + dp[i - 1][j - 1];
                } else {
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }
        return dp[m][n];
    }
