---
layout: post
title: "[LeetCode 91] Decode Ways"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/decode-ways/)

<div class="question-content">
            <p></p><p>
A message containing letters from <code>A-Z</code> is being encoded to numbers using the following mapping:
</p>

<pre>'A' -&gt; 1
'B' -&gt; 2
...
'Z' -&gt; 26
</pre>

<p>
Given an encoded message containing digits, determine the total number of ways to decode it.
</p>

<p>
For example,<br>
Given encoded message <code>"12"</code>,
it could be decoded as <code>"AB"</code> (1 2) or <code>"L"</code> (12).
</p>

<p>
The number of ways decoding <code>"12"</code> is 2.
</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This question is easy to think, but hard to write.__

Why? Because there are a lot of cases that the decode ways = 0. For example, input = "02" or "50". We must handle those cases well. Also, boundary cases can cause some trouble. 

### Solution

__DP solution, the transformation function is:__

> Count[i] = Count[i-1]  if only S[i-1] is valid

> Count[i] = Count[i-1] + Count[i-2] if S[i-1] and S[i-2] both valid

### Code

__First, my code.__ 

    public int numDecodings(String s) {
        int len = s.length();
		if (len == 0) return 0;
		// now len >= 1
		int[] dp = new int[len];
	    if (s.charAt(0) == '0') dp[0] = 0;
		else dp[0] = 1;
		if (len == 1) return dp[0];
		// now len >= 2
		for (int i = 1; i < len; i ++) {
			if (s.charAt(i) != '0') dp[i] += dp[i-1];
			int doubleDigit = Integer.parseInt(s.substring(i-1, i+1));
			if (s.charAt(i-1) != '0' && 1 <= doubleDigit && doubleDigit <= 26)
				if (i != 1) dp[i] += dp[i-2];
				else dp[i] += 1;
		}
		return dp[len - 1];
    }

__Second, code from [this blog](http://blog.csdn.net/u011095253/article/details/9248109).__ 

The only difference is an additional '1' at position 0 of the dp array. This helps simply the code a lot! 

    public int numDecodings(String s) {  
        int n = s.length();  
        if (n==0) return 0;  
        int[] dp = new int[n+1];  
        dp[0] = 1;  
        if (isValid(s.substring(0,1))) dp[1] = 1;  
        else dp[1] = 0;  
        for(int i=2; i<=n;i++){  
            if (isValid(s.substring(i-1,i)))  
                dp[i] = dp[i-1];  
            if (isValid(s.substring(i-2,i)))  
                dp[i] += dp[i-2];  
        }  
        return dp[n];  
    }  
      
    public boolean isValid(String s){  
        if (s.charAt(0)=='0') return false;  
        int code = Integer.parseInt(s);  
        return code>=1 && code<=26;  
    }
