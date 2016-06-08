---
layout: post
title: "[LeetCode 28] Implement strStr"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/implement-strstr/)

<div class="question-content">
<p></p><p>
Implement strStr().
</p>
<p>
Returns a pointer to the first occurrence of needle in haystack, or <b>null</b> if needle is not part of haystack.
</p><p></p>
</div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="white">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

There are 2 ways to solve this problem. 

1. __Most common way__ is using 2 nested loop 

1. Also can be solved by [KPM algorithm](http://en.wikipedia.org/wiki/Knuth%E2%80%93Morris%E2%80%93Pratt_algorithm)

### Solution

Standard solution is posted below. Read [this post](http://www.programcreek.com/2012/12/leetcode-implement-strstr-java/) for more.

As for KMP algo, I have to admit I am not able to do it. Plz refer to [this blog](http://discuss.leetcode.com/questions/76/implement-strstr) and [this blog](http://fisherlei.blogspot.sg/2012/12/leetcode-implement-strstr.html) for more! 

### My code 

    public class Solution {
        public int strStr(String haystack, String needle) {
            if (haystack == null || needle == null) {
                return -1;
            } else if (haystack.length() < needle.length()) {
                return -1;
            } else if (haystack.length() == 0 && needle.length() == 0) {
                return 0;
            }
            for (int i = 0; i <= haystack.length() - needle.length(); i++) {
                int j;
                // try to match part of haystack (starting from i) to needle 
                for (j = 0; j < needle.length(); j++) {
                    if (haystack.charAt(i + j) != needle.charAt(j)) {
                        break;
                    }
                }
                // if part of haystack (starting from i) matches needle 
                if (j == needle.length()) {
                    return i;
                }
                // if not match, proceed to next loop
            }
            return -1;
        }
    }
