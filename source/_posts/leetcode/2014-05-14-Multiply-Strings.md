---
layout: post
title: "[LeetCode 43] Multiply Strings "
comments: true
category: Leetcode

---

### Question

[link](http://oj.leetcode.com/problems/multiply-strings/)

<div class="question-content">
<p></p><p>Given two numbers represented as strings, return multiplication of the numbers as a string.</p>

<p>Note: The numbers can be arbitrarily large and are non-negative.</p><p></p>
</div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Solution

The basic idea is to __multiple numbers 1 by 1, and do decimal carry later__. Note the max length of result is (m+n) assuming 2 input are length m and n respectively. 

The code seems easy, but be careful when __converting result array into string__. That is, we should omit preceding '0's. 

Read [this blog](http://blog.csdn.net/fightforyourdream/article/details/17370495) for more. 

### My code 

    public class Solution {
        public String multiply(String num1, String num2) {
            if (num1 == null || num1.length() == 0) {
                return "0";
            } else if (num2 == null || num2.length() == 0) {
                return "0";
            }
            int len1 = num1.length();
            int len2 = num2.length();
            int len = len1 + len2;
            // eg. 99 * 999 = 98901
            int[] digits = new int[len];

            for (int i = 1; i <= len1; i++) {
                for (int j = 1; j <= len2; j++) {
                    // multiply the (i)th number from the end of num1
                    // with the (j)th number from the end of num2
                    int product = (num1.charAt(len1 - i) - '0') * (num2.charAt(len2 - j) - '0');
                    // this produce saves to the (i+j-1)th position in array
                    int ansPos = len + 1 - i - j;
                    digits[ansPos] += product;
                }
            }
            // answer is got and saved in digits array, but we
            // need to handle the carry numbers
            for (int i = len - 1; i > 0; i--) {
                digits[i - 1] += digits[i] / 10;
                digits[i] %= 10;
            }
            // last step is the print the answer, but mind the prefix 0s
            int p = 0;
            while (p < len && digits[p] == 0) {
                p++;
            }
            if (p == len) {
                return "0";
            } else {
                StringBuilder sb = new StringBuilder();
                while (p < len) {
                    sb.append(String.valueOf(digits[p++]));
                }
                return sb.toString();
            }
        }
    }
