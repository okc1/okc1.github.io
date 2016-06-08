---
layout: post
title: "[LeetCode 8] String to Integer (atoi) "
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/string-to-integer-atoi/)

<div class="question-content">
            <p></p><p>Implement <span style="font-family:monospace">atoi</span> to convert a string to an integer.</p>

<p><b>Hint:</b> Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.</p>

<p>
<b>Notes:</b> 
It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front. </p>

<div class="spoilers"><b>Requirements for atoi:</b>

<p>The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.</p>

<p>The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.</p>

<p>If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.</p>

<p>If no valid conversion could be performed, a zero value is returned. If the correct value is out of the range of representable values, INT_MAX (2147483647) or INT_MIN (-2147483648) is returned.
</p>
</div><p></p>
          </div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">5</td>
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
		<td bgcolor="yellow">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

This question is not difficult, but hard to get it right. Remember to handle all cases listed below: 

1. null or empty string
2. white spaces
3. +/- sign
4. calculate real value
5. return int.min or int.max

### Solution

__Use one loop to read through, and in the end do some checking__. There is a very good [explanation](http://www.programcreek.com/2012/12/leetcode-string-to-integer-atoi/) from online. 

This is a standard string question, and try think of some special test cases. 

### My code 

    public class Solution {
        public int atoi(String str) {
            if (str == null || str.length() == 0) {
                return 0;
            }
            int p = 0; 
            int len = str.length();
            // omit as many space as possible
            while (p < len) {
                if (str.charAt(p) != ' ') {
                    break;
                }
                p++;
            }
            int sign = 1;
            // check if there is a +/- sign at position p
            // if there is, store its value and advance p
            if (p == len) {
                return 0;
            } else if (str.charAt(p) == '+') {
                p++;
            } else if (str.charAt(p) == '-') {
                sign = -1;
                p++;
            }
            // check if position p have valid number
            if (p == len) {
                return 0;
            } else if (str.charAt(p) < '0' || str.charAt(p) > '9') {
                return 0;
            }
            // now position p is the start of numerical part.
            int q = p;
            while (q < len && str.charAt(q) >= '0' && str.charAt(q) <= '9') {
                q++;
            }
            String numPart = str.substring(p, q);
            // first, check if numPart is too long
            if (numPart.length() > 15) {
                if (sign == -1) {
                    return Integer.MIN_VALUE;
                } else {
                    return Integer.MAX_VALUE;
                }
            }
            // second, convert to numerical format and check value against Integer.MIN and MAX
            long num = sign * Long.parseLong(numPart);
            if (num > Integer.MAX_VALUE) {
                return Integer.MAX_VALUE;
            } else if (num < Integer.MIN_VALUE) {
                return Integer.MIN_VALUE;
            } else {
                return (int) num;
            }
        }
    }
