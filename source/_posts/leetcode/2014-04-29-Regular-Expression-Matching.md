---
layout: post
title: "[LeetCode 10] Regular Expression Matching "
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/regular-expression-matching/)

<div class="question-content">
<p></p><p>Implement regular expression matching with support for <code>'.'</code> and <code>'*'</code>.</p>

<pre>'.' Matches any single character.
'*' Matches <b>zero or more of the preceding</b> element.

The matching should cover the <b>entire</b> input string (not partial).

The function prototype should be:
bool isMatch(const char *s, const char *p)

Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "a*") → true
isMatch("aa", ".*") → true
isMatch("ab", ".*") → true
isMatch("aab", "c*a*b") → true
</pre><p></p>
</div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__Very important to note: Do not use DP__. Why? Because eg. "a\*b" will be considered as 2 parts: "a\*" part and "b" part. Because star is considered to be bundled with previous char, it gives us difficulty in determine the size of the DP array. Of course, we still can do it, but I see nobody have provided a nice DP solution online. Let's just forget about it for now. 

The solution I'm giving in this post, is to trim String and compare. 

__We only need to consider 2 cases__: 

One, the next char is NOT a star sign. This requires simply char compare. 

Two, the next char is a star sign, this will require some effort. 

### Solution

In case of one letter bundled with a star sign, we iterate thru all possible number of repetition of current char (from 0 until large), and check validation one by one.

A final important note, __this question very much looks like DP, but NOT DP__. 

### My code 

My code.

    public class Solution {
        public boolean isMatch(String s, String p) {
            // eg. s = "aab"  p = "c*a*b"
            return check(s, p, 0, 0);
        }

        private boolean check(String s, String p, int start1, int start2) {
            int len1 = s.length();
            int len2 = p.length();
            if (start1 == len1 && start2 == len2) {
                return true;
            } else if (start2 == len2) {
                // if p is used up, but still some letters left in s
                return false;
            }
            // check if there is * after start2 in p
            if (start2 == len2 - 1 || p.charAt(start2 + 1) != '*') {
                // if there is no *
                // match only 1 char
                if (start1 == len1) {
                    // unable to match single char because s is fully used up
                } else if (p.charAt(start2) != '.' && s.charAt(start1) != p.charAt(start2)) {
                    // if single char could not be matched
                    return false;
                } else {
                    // if single letter matches
                    return check(s, p, start1 + 1, start2 + 1);
                }
            } else {
                // if there is a * following start2
                if (check(s, p, start1, start2 + 2)) {
                    // the letter in p represent 0 chars
                    return true;
                } else {
                    // the letter in p represent 1 or more chars
                    // advance start1 until the end of s
                    while (start1 < len1) {
                        // check if the char matches
                        if (p.charAt(start2) != '.' && s.charAt(start1) != p.charAt(start2)) {
                            break;
                        }
                        if (check(s, p, start1 + 1, start2 + 2)) {
                            return true;
                        }
                        start1++;
                    }
                }
            }
            return false;
        }
    }

A much shorter version from [someone else](http://www.programcreek.com/2012/12/leetcode-regular-expression-matching-in-java/) making use of __String.substring()__. I refactored a bit. 

    public class Solution {
        public boolean isMatch(String s, String p) {
            // s is normal string, and p is regex string
            if (p.length() == 0) {
                return s.length() == 0;
            } else if (p.length() < 2 || p.charAt(1) != '*') {
                // if 2nd char in p is not '*', then match character
                if (s.length() == 0) {
                    return false;
                } else if (p.charAt(0) != '.' && s.charAt(0) != p.charAt(0)) {
                    return false;
                } else {
                    return isMatch(s.substring(1), p.substring(1));
                }
            } else {
                // if 2nd char in p is '*', then iterate all position repetitions
                char repeatLetter = p.charAt(0);
                for (int i = 0; i <= s.length(); i++) {
                    // i is the number of repetition of repeatLetter, start from 0
                    if (i > 0 && repeatLetter != s.charAt(i - 1)
                            && repeatLetter != '.') {
                        break;
                    } else {
                        if (isMatch(s.substring(i), p.substring(2))) {
                            return true;
                        }
                    }
                }
                return false;
            }
        }
    }
