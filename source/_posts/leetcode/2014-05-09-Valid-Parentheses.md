---
layout: post
title: "[LeetCode 20] Valid Parentheses"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/valid-parentheses/)

<div class="question-content">
            <p></p><p>Given a string containing just the characters <code>'('</code>, <code>')'</code>, <code>'{'</code>, <code>'}'</code>, <code>'['</code> and <code>']'</code>, determine if the input string is valid.</p>

<p>The brackets must close in the correct order, <code>"()"</code> and <code>"()[]{}"</code> are all valid but <code>"(]"</code> and <code>"([)]"</code> are not.</p>
<p></p>
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
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

Either stack or string would work.

### Solution

The code is easy. 

### My code 

    public class Solution {
        public boolean isValid(String s) {
            if (s == null || s.length() == 0) {
                return false;
            }
            Stack<Character> stack = new Stack<Character>();
            // process s char by char
            for (char c: s.toCharArray()) {
                if (c == '(' || c == '[' || c == '{') {
                    stack.push(c);
                } else {
                    if (stack.isEmpty()) {
                        // eg. input = "())))"
                        return false;
                    }
                    char top = stack.pop();
                    if (Math.abs(top - c) > 2) {
                        // parentheses does not match
                        return false;
                    }
                }
            }
            // after this, stack should be empty (if parentheses valid)
            return stack.isEmpty();
        }
    }
