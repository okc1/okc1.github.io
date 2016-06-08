---
layout: post
title: "[LeetCode 17] Letter Combinations of a Phone Number"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/letter-combinations-of-a-phone-number/)

<div class="question-content">
            <p></p><p>Given a digit string, return all possible letter combinations that the number could represent.
</p>

<p>
A mapping of digit to letters (just like on the telephone buttons) is given below.</p>
<p><img src="http://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png"></p>

<pre><b>Input:</b>Digit string "23"
<b>Output:</b> ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
</pre>

<p>
<b>Note:</b><br>
Although the above answer is in lexicographical order, your answer could be in any order you want.
</p><p></p>
</div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="yellow">3</td>
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

There are 2 considerations associated with this question: 

1. How to convert an number into a String (i.e. 2->'abc' etc.) 

1. How the search works. 

#### Convert number to string 

There are 2 way: __math way__, or the __hashmap way__. 

My initial idea is to calculate it mathematically: 

    private String getLetters(int key) {
        if (key <= 1 || key >= 10) return "";
        // key must be in the range of [2,9]
        char first = (char) ('a' + (key - 2) * 3);
        if (key >= 8) first++;
        String letters = "";
        for (int i = 0; i < 4; i++) {
            if (i == 3 && !(key == 7 || key == 9)) {
                break;
            }
            letters += first++;
        }
        return letters;
    }
    String letters = getLetters('3' - '0');

However, most people would use HashMap. It's not the main issue anyway, so using HashMap is fine. 

### Solution

This is very typical "Permutation" question. Need to memorize clearly. 

Refer to [ninechap](http://www.ninechapter.com//solutions/letter-combinations-of-a-phone-number/) for the solution and a piece of very standard code. 

### My code 

    public class Solution {
        public List<String> letterCombinations(String digits) {
            List<String> ans = new ArrayList<String>();
            if (digits == null || digits.length() == 0) {
                ans.add("");
                return ans;
            }
            int len = digits.length();
            // this type of DFS question is very standardized
            helper(ans, "", digits, 0, len);
            return ans;
        }

        private void helper(List<String> ans, String path, String digits, int pos, int len) {
            if (pos == len) {
                ans.add(path);
                return;
            }
            // check the char at position 'pos', and find all possible letters to insert
            String possibleLetters = getLetters(digits.charAt(pos));
            for (char letter: possibleLetters.toCharArray()) {
                helper(ans, path + letter, digits, pos + 1, len);
            }
        }

        private String getLetters(char digit) {
            // first convert char to integer
            int index = digit - '0';
            String[] map = new String[] {
                " ",
                "",
                "abc",
                "def",
                "ghi",
                "jkl",
                "mno",
                "pqrs",
                "tuv",
                "wxyz"
            };
            // second, find corresponding string from map
            return map[index];
        }
    }
