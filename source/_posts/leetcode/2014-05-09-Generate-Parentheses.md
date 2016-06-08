---
layout: post
title: "[LeetCode 22] Generate Parentheses "
comments: true
category: Leetcode

---

### Question 

[link](https://oj.leetcode.com/problems/generate-parentheses/)

<div class="question-content">
            <p></p><p>
Given <i>n</i> pairs of parentheses, write a function to generate all combinations of well-formed parentheses.
</p>

<p>
For example, given <i>n</i> = 3, a solution set is:
</p>
<p>
<code>"((()))", "(()())", "(())()", "()(())", "()()()"</code>
</p><p></p>
</div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Solution

Very standard permutation search. You can read more from [this link](http://www.geeksforgeeks.org/print-all-combinations-of-balanced-parentheses/).

### My code 

    public class Solution {
        public List<String> generateParenthesis(int n) {
            List<String> ans = new ArrayList<String>();
            if (n == 0) {
                return ans;
            }
            helper(ans, "", n, n);
            return ans;
        }

        private void helper(List<String> ans, String path, int left, int right) {
            if (left == 0 && right == 0) {
                ans.add(path);
                return;
            }
            // add either left or right parenthese
            if (left > 0) {
                helper(ans, path + "(", left - 1, right);
            }
            if (right > left) {
                helper(ans, path + ")", left, right - 1);
            }
        }
    }
