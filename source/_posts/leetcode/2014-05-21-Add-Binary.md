---
layout: post
title: "[LeetCode 67] Add Binary"
comments: true
category: Leetcode

---


### Question 
[link](http://oj.leetcode.com/problems/add-binary/)

<div class="question-content">
            <p></p><p>
Given two binary strings, return their sum (also a binary string).
</p>

<p>
For example,<br>
a = <code>"11"</code><br>
b = <code>"1"</code><br>
Return <code>"100"</code>.
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
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is an easy question__. Pure coding. 

There are some boundary issues during my first attempt. And special note to the trim() operation after "String.valueOf(ans)", it's easy to omit. 

### My code


    public String addBinary(String a, String b) {
        int m = a.length(), n = b.length();
        char[] ans = new char[Math.max(m, n) + 1];
        int p = m - 1, q = n - 1, r = ans.length - 1;
        int carry = 0;
        while (r >= 0) {
            if (p >= 0)
                ans[r] += a.charAt(p--) - '0';
            if (q >= 0)
                ans[r] += b.charAt(q--) - '0';
            int temp = ans[r] + carry;
            ans[r] = (char) (temp % 2 + '0');
            carry = temp / 2;
            r--;
        }
        if (ans[0] == '0')
            ans[0] = ' ';
        return String.valueOf(ans).trim();
    }
