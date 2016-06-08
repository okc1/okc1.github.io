---
layout: post
title: "[LeetCode 38] Count and Say"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/count-and-say/)

<div class="question-content">
<p></p><p>The count-and-say sequence is the sequence of integers beginning as follows:<br>
<code>1, 11, 21, 1211, 111221, ...</code>
</p>

<p>
<code>1</code> is read off as <code>"one 1"</code> or <code>11</code>.<br>
<code>11</code> is read off as <code>"two 1s"</code> or <code>21</code>.<br>
<code>21</code> is read off as <code>"one 2</code>, then <code>one 1"</code> or <code>1211</code>.<br>
</p>

<p>
Given an integer <i>n</i>, generate the <i>n</i><sup>th</sup> sequence.
</p>

<p>
Note: The sequence of integers will be represented as a string.
</p>
</div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="lime">2</td>
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
		<td bgcolor="white">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Solution

__This is a implementation question, not difficult__. 

### My code

code 1

    public class Solution {
        public String countAndSay(int n) {
            String num = "1";
            for (int i = 1; i < n; i++) {
                num = say(num);
            }
            return num;
        }

        private String say(String input) {
            // 21 -> 1211
            int len = input.length();
            String output = "";
            int left = 0;
            int right = 0;
            while (right < len) {
                left = right;
                // forward right until right pointer to a different value
                // compared to that pointed by left pointer
                while (right < len && input.charAt(left) == input.charAt(right)) {
                    right++;
                }
                output += String.valueOf(right - left);
                output += input.charAt(left);
            }
            return output;
        }
    }

code 2

    public String countAndSay(int n) {
        String s = "1";
        for (int i = 2; i <= n; i ++) {
            char[] nums = s.toCharArray();
            String newS = "";
            int len = nums.length, left = 0, right = 0;
            while (right < len) {
                while (right < len && nums[left] == nums[right]) right ++;
                newS += (right - left) + "" + nums[left];
                left = right;
            }
            s = newS;
        }
        return s;
    }
