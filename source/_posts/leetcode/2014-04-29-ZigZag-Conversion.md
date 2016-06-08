---
layout: post
title: "[LeetCode 6] ZigZag Conversion "
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/zigzag-conversion/)

<div class="question-content">
<p></p><p>
The string <code>"PAYPALISHIRING"</code> is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)
</p><pre>
P   A   H   N
A P L S I I G
Y   I   R
</pre>

And then read line by line: <code>"PAHNAPLSIIGYIR"</code><p></p>

<p>
Write the code that will take a string and make this conversion given a number of rows:

</p><pre>string convert(string text, int nRows);</pre>

<code>convert("PAYPALISHIRING", 3)</code> should return <code>"PAHNAPLSIIGYIR"</code>.
<p></p><p></p>
</div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="white">1</td>
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
		<td bgcolor="yellow">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Solution

__Two ways to work out this problem__.

Solution 1. Insert string s vertically into a 2d array, char by char. After this is finished, make the result string by reading the 2d array horizontally. See code 1 below. 

Solution 2. Calculate and find out (in sequence) which char from s should be inserted into the result list. Then build the result list directly. See code 2 below. 

### My code 

One. Fill in the whole string, then parse the result. 

    public class Solution {
        public String convert(String s, int nRows) {
            if (s == null || s.length() == 0 || nRows < 1) {
                return "";
            } else if (nRows == 1) {
                return s;
            }
            int len = s.length();
            int grpSize = nRows * 2 - 2;
            int numGrp = (len - 1) / grpSize + 1;
            String[][] array = new String[nRows][numGrp * 2];
            // fill in string s into array, one group after another
            int p = 0;
            // for each group
            for (int i = 0; i < numGrp; i++) {
                // for each vertical index (left col), fill in one letter from s
                for (int j = 0; j < nRows; j++) {
                    // if s is used up, break
                    if (p == len) {
                        break;
                    }
                    array[j][i * 2] = "" + s.charAt(p);
                    p++;
                }
                // for each vertical index (right col), fill in one letter from s
                for (int j = nRows - 2; j > 0; j--) {
                    // if s is used up, break
                    if (p == len) {
                        break;
                    }
                    array[j][i * 2 + 1] = "" + s.charAt(p);
                    p++;
                }
            }
            // now convert array[][] into final string and return answer
            StringBuilder sb = new StringBuilder();
            for (int i = 0; i < array.length; i++) {
                for (int j = 0; j < array[0].length; j++) {
                    if (array[i][j] == null || array[i][j].length() == 0) {
                        continue;
                    } else {
                        sb.append(array[i][j]);
                    }
                }
            }
            return sb.toString();
        }
    }

Two. Pick the correct char and form the result string, and fill it in the result string. 

    public class Solution {
        public String convert(String s, int nRows) {
            if (nRows <= 1)
                return s;
            int eachPattern = 2 * nRows - 2;
            int numPatterns = (s.length() - 1) / eachPattern + 1;
            StringBuilder ans = new StringBuilder();
            for (int j = 0; j < nRows; j++) {
                for (int i = 0; i < numPatterns; i++) {
                    ans.append(find(s, eachPattern, i, j));
                    if (j != 0 && j != nRows - 1)
                        ans.append(find(s, eachPattern, i, 2 * (nRows - 1) - j));
                }
            }
            return ans.toString();
        }

        private String find(String s, int eachPattern, int i, int j) {
            // find (j)th element from (i)th pattern
            int temp = eachPattern * i + j;
            if (temp < s.length())
                return s.substring(temp, temp + 1);
            return "";
        }
    }
