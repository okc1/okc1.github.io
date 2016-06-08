---
layout: post
title: "[LeetCode 65] Valid Number (unsolvable)"
comments: true
category: Leetcode
tags: [ unsolvable ]
---

### Question 

[link](http://oj.leetcode.com/problems/valid-number/)

<div class="question-content">
            <p></p><p>Validate if a given string is numeric.</p>

<p>
Some examples:<br>
<code>"0"</code> =&gt; <code>true</code><br>
<code>"   0.1  "</code> =&gt; <code>true</code><br>
<code>"abc"</code> =&gt; <code>false</code><br>
<code>"1 a"</code> =&gt; <code>false</code><br>
<code>"2e10"</code> =&gt; <code>true</code><br>
</p>

<p><b>Note:</b> It is intended for the problem statement to be ambiguous. You should gather all requirements up front before implementing one.
</p><p></p>
          </div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">unsolvable</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Solution

I am unable to solve this problem, but I found a [quite good solution](http://leetcodenotes.wordpress.com/2013/11/23/leetcode-valid-number/). I post the code below. 

### My code

    public boolean isNumber(String s) {
        s = s.trim(); 
        if (s.length() > 0 && s.charAt(s.length() - 1) == 'e')
            return false; //avoid "3e" which is false
        String[] t = s.split("e");
        if (t.length == 0 || t.length > 2) return false;
        boolean res = valid(t[0], false);
        if (t.length > 1) res = res && valid(t[1], true);
        return res;
    }

    private boolean valid(String s, boolean hasDot) {
        if (s.length() > 0 && (s.charAt(0) == '+' || s.charAt(0) == '-')) 
            s = s.substring(1); //avoid "1+", "+", "+."
        char[] arr = s.toCharArray();
        if (arr.length == 0 || s.equals(".")) return false;
        for (int i = 0; i < arr.length; i++) {
            if (arr[i] == '.') {
                if (hasDot) return false;
                hasDot = true;
            } else if (!('0' <= arr[i] && arr[i] <= '9'))
                return false;
        }
        return true;
    }

