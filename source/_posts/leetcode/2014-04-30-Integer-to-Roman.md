---
layout: post
title: "[LeetCode 12] Integer to Roman"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/integer-to-roman/)

<div class="question-content">
<p></p><p>Given an integer, convert it to a roman numeral.
</p>
<p>Input is guaranteed to be within the range from 1 to 3999.</p><p></p>
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
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

Symbol | Value
|:-------------:|:-------------:|
I|1
V|5
X|10
L|50
C|100
D|500
M|1,000

Though [Roman numerals](http://en.wikipedia.org/wiki/Roman_numerals) looks complex, it's actually converted bit by bit. For example 207=>CCVII. We can then construct __the following relationship table__: 

Base/number|Number(1)|Number(5)|Number(10)
|:-------------:|:-------------:|:-------------:|:-------------:|
1|I|V|X
10|X|L|C
100|C|D|M
1000|M|n.a.|n.a.

So for each number, just do convert according to the above table. 

> 9=>IX

> 400=>CD. 

The question states that input is less than 3999. 

### Analysis

Before I present my solution, there is a very short code written by stackoverflow user [bhlangonijr](http://stackoverflow.com/a/19759564). This method __makes use of Java [TreeMap.floorKey](http://goo.gl/e8ryim)__. Read it ONLY if you are interested! 

> TreeMap.floorKey - Returns the greatest key less than or equal to the given key, or null if there is no such key.

    public String intToRoman3(int num) {
        TreeMap<Integer, String> map = new TreeMap<Integer, String>();
        map.put(1000, "M");
        map.put(900, "CM");
        map.put(500, "D");
        map.put(400, "CD");
        map.put(100, "C");
        map.put(90, "XC");
        map.put(50, "L");
        map.put(40, "XL");
        map.put(10, "X");
        map.put(9, "IX");
        map.put(5, "V");
        map.put(4, "IV");
        map.put(1, "I");
        int l = map.floorKey(num);
        if (num == l) {
            return map.get(num);
        }
        return map.get(l) + intToRoman3(num - l);
    }

### Solution

I will present 2 solutions below. 

First is an iterative solution. It's comparatively shorter, and enjoys beter performance. 

Second is my new idea. It has improved readability, but slightly worse performance, because it's recursive. 

### My code 

Code 1, iterative. 

    public class Solution {

        char[][] roman = {
            { 'I', 'V', 'X' }, 
            { 'X', 'L', 'C' }, 
            { 'C', 'D', 'M' },
            { 'M', '*', '*' } 
        };

        public String intToRoman(int num) {
            String ans = "";
            int base = 1, count = 0, temp = num;
            while (temp > 1) {
                base *= 10;
                count++;
                temp /= 10;
            }
            while (base > 0) {
                int cur = num / base;
                // now convert cur into roman string
                if (cur >= 6 && cur <= 8) {
                    ans += roman[count][1];
                    cur = cur % 5;
                }
                if (cur >= 1 && cur <= 3)
                    for (int k = 0; k < cur; k++)
                        ans += roman[count][0];
                else if (cur == 5)
                    ans += roman[count][1];
                else if (cur == 4)
                    ans += roman[count][0] + "" + roman[count][1];
                else if (cur == 9)
                    ans += roman[count][0] + "" + roman[count][2];
                num = num % base;
                base /= 10;
                count--;
            }
            return ans;
        }

    }

Code 2, recursive. 

    public class Solution {

        HashMap<Integer, String> map = new HashMap<Integer, String>();

        public String intToRoman(int num) {

            map.put(1000, "M");
            map.put(500, "D");
            map.put(100, "C");
            map.put(50, "L");
            map.put(10, "X");
            map.put(5, "V");
            map.put(1, "I");

            String roman = "";
            int base = 1000;
            int digit = 0;
            while (num != 0) {
                digit = num / base;
                num = num % base;
                roman = roman + convert(digit, base);
                base /= 10;
            }
            return roman;
        }

        private String convert(int digit, int base) {
            String ans = "";
            String one = map.get(base);
            String five = map.get(base * 5);
            if (digit == 0) {
                return "";
            } else if (digit <= 3) {
                for (int i = 0; i < digit; i++) {
                    ans += one;
                }
            } else if (digit == 4) {
                ans += one;
                ans += convert(5, base);
            } else if (digit == 5) {
                ans += five;
            } else if (digit <= 8) {
                ans += convert(5, base);
                ans += convert(digit - 5, base);
            } else if (digit == 9) {
                ans += one;
                ans += convert(1, base * 10);
            }
            return ans;
        }
    }
