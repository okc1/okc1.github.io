---
layout: post
title: "[LeetCode 139] Word Break"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/word-break/)

<div class="question-content bg-color bg-img font-color">
            <p class="font-color"></p><p class="font-color">
Given a string <i>s</i> and a dictionary of words <i>dict</i>, determine if <i>s</i> can be segmented into a space-separated sequence of one or more dictionary words.
</p>

<p class="font-color">For example, given<br>
<i>s</i> = <code>"leetcode"</code>,<br>
<i>dict</i> = <code>["leet", "code"]</code>.
</p>

<p class="font-color">
Return true because <code>"leetcode"</code> can be segmented as <code>"leet code"</code>.
</p><p class="font-color"></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a standard DP question__. 

### Solution

I see a lot of people solve this DP problem with 2D array. It actually requires only 1D aray. 

Declare an boolean array of (input string length) + 1, and dp[i] mean whether or not subtring(0,i) is work-breakable. Then the problem is clear and easy. 

Pay attention to index while coding. 

### Code

__my code__

    public boolean wordBreak(String s, Set<String> dict) {
        int len = s.length();
        if (len == 0 || dict.isEmpty())  {
            return false;
        }
        boolean[] dp = new boolean[len + 1];
        dp[0] = true;
        for (int i = 1; i <= len; i ++)  {
            for (int j = 0; j < i; j ++)  {
                if (dp[j] && dict.contains(s.substring(j, i)))  {
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[len];
    }
