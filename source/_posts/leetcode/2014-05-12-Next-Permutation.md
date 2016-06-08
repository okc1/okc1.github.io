---
layout: post
title: "[LeetCode 31] Next Permutation"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/next-permutation/)

<div class="question-content">
            <p></p><p>
Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.
</p>
<p>
If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).
</p>
<p>
The replacement must be in-place, do not allocate extra memory.
</p>
<p>
Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.<br>
<code>1,2,3</code> → <code>1,3,2</code><br>
<code>3,2,1</code> → <code>1,2,3</code><br>
<code>1,1,5</code> → <code>1,5,1</code><br>
</p><p></p>
          </div>
### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="red">5</td>
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

### Analysis

The image below explains the solution very well (for the input number "687432").

{% img middle /assets/images/next_permutation.png %}

### Solution

Read [this blog](http://blog.csdn.net/havenoidea/article/details/12176737) for a very nice piece of code. 

The following code is written by me. 

### My code 

    public class Solution {
        public void nextPermutation(int[] num) {
            if (num == null || num.length <= 1) {
                return;
            }
            int len = num.length;
            int p = len - 2;
            // note that when values are equals, proceed the pointer! 
            // same for line 22
            while (p >= 0 && num[p] >= num[p + 1]) {
                // move p to left as long as its value is larger than next num
                // we want to find the end of increasing sequence (from end to start)
                p--;
            }
            if (p == -1) {
                // the input is a strictly decreasing sequence
                Arrays.sort(num);
                return;
            }
            // replace number at p with an larger value found in the right of p
            int w = len - 1;
            while (num[w] <= num[p]) {
                w--;
            }
            // ok, now swap number at p and w
            swop(num, p, w);
            // reverse all numbers to the right of p
            reverse(num, p + 1, len - 1);
        }

        private void swop(int[] num, int a, int b) {
            int temp = num[a];
            num[a] = num[b];
            num[b] = temp;
        }

        private void reverse(int[] num, int a, int b) {
            while (a < b) {
                swop(num, a++, b--);
            }
        }
    }
