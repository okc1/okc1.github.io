---
layout: post
title: "[LeetCode 29] Divide Two Integers"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/divide-two-integers/)

<div class="question-content">
            <p></p><p>
Divide two integers without using multiplication, division and mod operator.
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
		<td bgcolor="red">4</td>
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

__This question might be more difficult than you thought__. So do not overlook it because of its seemingly simple description. First of all, please refer to __[Fundamental] Java Bit Operation__ for information on bit operators. 

And __remember... overflow can happen__, especially when you dealing with Integer.MAX_VALUE and Integer.MIN_VALUE. 

### Solution

This solution is __a while loop that keeps subtracting (divisor * (2 ^ n)) from dividend__. You can find a good solution from [this blog](http://leetcodenotes.wordpress.com/2013/10/19/divide-two-integers/). 

### code 

    public class Solution {
        public int divide(int dividend, int divisor) {
            int sign = 1;
            long x = dividend;
            long y = divisor;
            if (x < 0) {
                x = x * -1;
                sign *= -1;
            }
            if (y < 0) {
                y = y * -1;
                sign *= -1;
            }
            return divide(sign, x, y);
        }

        private int divide(int sign, long x, long y) {
            // both x and y are positive numbers
            if (x < y) {
                return 0;
            }
            long quotient = 0;
            long partialQuotient;
            long partialSubtract;
            while (x >= y) {
                // the idea is to subtract a certain times of x from y
                // and save the remainder value back to x
                partialQuotient = 1;
                partialSubtract = y;
                while ((partialSubtract << 1) <= x) {
                    partialQuotient <<= 1; // doubles quotient
                    partialSubtract <<= 1; // doubles subtraction
                }
                x -= partialSubtract;
                quotient += partialQuotient;
            }
            long finalQuo = sign * quotient;
            if (finalQuo < Integer.MIN_VALUE || finalQuo > Integer.MAX_VALUE) {
                return Integer.MAX_VALUE;
            } else {
                return (int) finalQuo;
            }
        }
    }