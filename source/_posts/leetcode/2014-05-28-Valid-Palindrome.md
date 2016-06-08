---
layout: post
title: "[LeetCode 125] Valid Palindrome"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/valid-palindrome/)

<div class="question-content">
            <p></p><p>
Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.
</p>

<p>
For example,<br>
<code>"A man, a plan, a canal: Panama"</code> is a palindrome.<br>
<code>"race a car"</code> is <i>not</i> a palindrome.
</p>

<p>
<b>Note:</b><br>
Have you consider that the string might be empty? This is a good question to ask during an interview.</p>
<p>
For the purpose of this problem, we define empty string as valid palindrome.
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
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

Wow, it's frequency 5! 

__This is a very classic and easy question__. 

### Code

    public boolean isPalindrome(String s) {
        int len = s.length();
        s = s.toLowerCase();
        int left = 0, right = len - 1;
        while (left < right) {
            while (left < len && !isAlphanumeric(s.charAt(left)))
                left ++;
            while (right >= 0 && ! isAlphanumeric(s.charAt(right)))
                right --;
            if (left == len && right == -1) return true;
            if (left == len || right == -1) return false;
            if (s.charAt(left) != s.charAt(right)) 
                return false;
            left ++;
            right --;
        }
        return true;
    }
    
    private boolean isAlphanumeric(char c) {
        return ('a' <= c && c <= 'z') 
            || ('0' <= c && c <= '9');
    }
