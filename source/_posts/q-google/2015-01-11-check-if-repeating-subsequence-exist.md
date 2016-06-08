---
layout: post
title: "[Google] Check if repeating subsequence exists "
comments: true
category: q-google

---

### Question 

[link](http://www.careercup.com/question?id=5931067269709824)

> Given a string, find if there is any sub-sequence that repeats itself. Do not reuse any char. 

> Eg: 

    1. abab <------yes, ab is repeated
    2. abba <---- No, a and b follow different order 
    3. acbdaghfb <-------- yes, a followed by b twice 
    4. abcdacb <----- yes, a followed by b twice 

> Note that no char should be reused. I.e. "aab" is a false. 

### Solution

This looks like a question without any clue. However, this actually is a modified version of __[LintCode] Longest Common Subsequence__. 

Look at that question: there's 2 input string, and they match char-by-char. For this question, we are simply __matching input string with input string itself__. And chars should be match __ONLY__ at different positions, that's the key. As pointed out by the [top comment](http://www.careercup.com/question?id=5931067269709824): 

> Now we can modify the longest_common_subsequence(a, a) to find the value of the longest repeated subsequence in a by excluding the cases when i == j

### Code

	public boolean checkRepeatSubseq(String input) {
		int len = input.length();
		int[][] dp = new int[len + 1][len + 1];
		// dp[i][j] denotes the length of subseq between 2 strings:
		// 1. first i chars of input
		// 2. first j chars of input
		for (int i = 1; i <= len; i++) {
			for (int j = i; j <= len; j++) {
				if (i != j && input.charAt(i - 1) == input.charAt(j - 1)) {
					int temp = Math.max(dp[i - 1][j], dp[i][j - 1]);
					dp[i][j] = Math.max(temp, dp[i - 1][j - 1] + 1);
				} else {
					dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
				}
			}
		}
		return dp[len][len] >= 2;
	}
