---
layout: post
title: "[LeetCode 9] Palindrome Number "
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/palindrome-number/)

<div class="question-content">
<p></p><p>Determine whether an integer is a palindrome. Do this without extra space.</p>

<div class="spoilers" style="display: block;"><b>Some hints:</b>

<p>Could negative integers be palindromes? (ie, -1)</p>

<p>If you are thinking of converting the integer to string, note the restriction of using extra space.</p>

<p>You could also try reversing an integer. However, if you have solved the problem "Reverse Integer", you know that the reversed integer might overflow. How would you handle such case?</p>

<p>There is a more generic way of solving this problem.</p>

</div><p></p>
</div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="white">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

This question is easy, and very similar to the "Reverse Integer" question. __Simpliest solution is to just reverse the integer__ and compare with original number. 

But again, reversing the integer have chances of __overflow__. How do we work this out? 

### Solution

First, same as previous post __[LeetCode 7] Reverse Integer__, we can use Long type to handle the overflow issues. 

Second, __we can also do direct compare__ to always compare the head and tail of the number. No numerical type conversion is needed. I came up with idea previously, and code is posted below. 

### My code 

Use Long type:

    public class Solution {
        public boolean isPalindrome(int x) {
            if (x < 0) {
                return false;
            }
            long rev = 0;
            long original = x;
            while (x != 0) {
                rev = rev * 10 + (x % 10);
                x = x / 10;
            }
            return original == rev;
        }
    }

Compare head and tail:

    public boolean isPalindrome(int x) {
        if (x < 0) {
            return false;
        }
        int divide = 1;
        while (x / divide >= 10) {
            divide *= 10;
        }
        int head = 0, tail = 0;
        while (divide > 0) {
            head = x / divide;
            tail = x % 10;
            if (head != tail) {
                return false;
            }
            x = x % divide / 10;
            divide /= 100;
        }
        return true;
    }
