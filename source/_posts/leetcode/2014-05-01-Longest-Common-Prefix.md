---
layout: post
title: "[LeetCode 14] Longest Common Prefix "
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/longest-common-prefix/)

<div class="question-content">
            <p></p><p>Write a function to find the longest common prefix string amongst an array of strings.
</p><p></p>
</div>

### Stats 

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="white">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis 

__Straight-forward solution.__ Will not go into details. 

However, there's another more generalized [__LCP array__](http://en.wikipedia.org/wiki/LCP_array) which is solved by use of [Trie](http://en.wikipedia.org/wiki/Trie). 

### Solution 

The code explains itself. 

### My code 

    public class Solution {
        public String longestCommonPrefix(String[] strs) {
            if (strs == null || strs.length == 0) {
                return "";
            }
            int p;
            for (p = 0; p < strs[0].length(); p++) {
                char c = strs[0].charAt(p);
                // check all strings in array strs
                for (int i = 0; i < strs.length; i++) {
                    if (p == strs[i].length()) {
                        return strs[i];
                    } else if (c != strs[i].charAt(p)) {
                        return strs[i].substring(0, p);
                    }
                }
                // if all strings have the same prefix
                // continue checking it
            }
            // first string in array strs is the shortest common prefix
            return strs[0];
        }
    }
