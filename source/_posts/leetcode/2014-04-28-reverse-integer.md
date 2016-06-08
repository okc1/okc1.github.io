---
layout: post
title: "[LeetCode 7] Reverse Integer "
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/reverse-integer/)

<div class="question-content">
<p></p><p>Reverse digits of an integer.</p>

<p style="font-family:monospace">
<b>Example1:</b> x =  123, return  321<br>
<b>Example2:</b> x = -123, return -321
</p>

<div class="spoilers"><b>Have you thought about this?</b>
<p>Here are some good questions to ask before coding. Bonus points for you if you have already thought through this!</p>
<p>If the integer's last digit is 0, what should the output be? ie, cases such as 10, 100.</p>
<p>Did you notice that the reversed integer might overflow? Assume the input is a 32-bit integer, then the reverse of 1000000003 overflows. How should you handle such cases?</p>
<p>Throw an exception? Good, but what if throwing an exception is not an option? You would then have to re-design the function (ie, add an extra parameter).</p>
</div><p></p>
</div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__There're 2 points that are tricky.__

__First, overflow issue__. Look at the following overflow case for Java int: 

	+300,000,000 * 10 returns -1294967296
    +600,000,000 * 10 returns +1705032704
	-300,000,000 * 10 returns +1294967296
	-600,000,000 * 10 returns -1705032704
    note that max integer is 2,147,483,647

We can observe that if overflow happens, __the result is definitely wrong__. The result can be either positive or negative. 

So, from just +/- sign of the result, we can't identify an overflow (then how to solve this problem??). 

__Another interesting thing to note: we actually do not need to handle negative sign__. The sign can be preserved during the conversion. Read [this post](http://fisherlei.blogspot.sg/2012/12/leetcode-reverse-integer.html) for more. 

Without considering overflow, the following code can (almost) work fine: 

    public int reverse2(int x) {
        int reverse = 0;
        while (x != 0) {
            reverse = reverse * 10 + x % 10;
            x /= 10;
        }
        return reverse;
    }

### Solution

__Two solutions__: 1. use long data type. 2. check if ret > 214748364 or ret < –214748364 before multiplying by 10. 

### My code 

First, using long type to avoid overflow.

    public class Solution {
        public int reverse(int x) {
            int sign = 1;
            long abs = x;
            long rev = 0;
            if (x < 0) {
                sign = -1;
                abs = 0 - abs;
            }
            // now remove numbers from abs one by one
            // and put these numbers into rev
            while (abs != 0) {
                rev *= 10;
                rev += abs % 10;
                abs /= 10;
            }
            if (rev > Integer.MAX_VALUE) {
                return 0;
            } else {
                return sign * (int) rev;
            }
        }
    }

Second, do boundary check in every step. Suggested by Leetcode official book. 

Note that max integer is 2,147,483,647

    public class Solution {

        public int reverse(int x) {
            int ret = 0;
            while (x != 0) {
                // handle overflow/underflow
                if (Math.abs(ret) > 214748364) {
                    return 0;
                }
                ret = ret * 10 + x % 10;
                x /= 10;
            }
            return ret;
        }
    }
