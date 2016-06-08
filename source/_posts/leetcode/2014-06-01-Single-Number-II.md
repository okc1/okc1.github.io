---
layout: post
title: "[LeetCode 137] Single Number II"
comments: true
category: Leetcode

---

### Question 
[link](https://oj.leetcode.com/problems/single-number-ii/)

<div class="question-content bg-color bg-img font-color">
            <p class="font-color"></p><p class="font-color">
Given an array of integers, every element appears <i>three</i> times except for one. Find that single one.
</p>

<p class="font-color">
<b>Note:</b><br>
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?
</p><p class="font-color"></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>$
		<td>Time to use</td>
		<td bgcolor="red">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is an extremely difficult question__. There are 2 solutions (both are bit manipulation). 

### Solution

__First solution comes from [this forum](https://oj.leetcode.com/discuss/857/constant-space-solution)__. 

> A straightforward implementation is to use an array of size 32 to keep track of the total count of ith bit.

A more detailed [explanation](http://leetcodesolutions.blogspot.sg/2013/10/single-number-ii.html): 

<blockquote cite="http://leetcodesolutions.blogspot.sg/2013/10/single-number-ii.html">
    <div >
        <span style="font-family: Times, Times New Roman, serif;" class="font-color">For eg : A = [ 2, 3, 3, 3]</span>
    </div>
    <div >
        <span style="font-family: Times, Times New Roman, serif;" class="font-color">We count the number of 1s for each bit position. Then find <i>mod 3 </i>of each of them. The bit positions having <i>mod 3 </i>&nbsp;equal to one are the bits that are set due to the number occurring once.</span>
    </div>
    <div >
        <span style="font-family: Times, Times New Roman, serif;" class="font-color">Writing the Binary Representation of the numbers.</span>
    </div>
    <div >
        <span style="font-family: Times, Times New Roman, serif;" class="font-color">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 0 0 1 0</span>
    </div>
    <div >
        <span style="font-family: Times, Times New Roman, serif;" class="font-color">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 0 0 1 1</span>
    </div>
    <div >
        <span style="font-family: Times, Times New Roman, serif;" class="font-color">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 0 0 1 1</span>
    </div>
    <div >
        <span style="font-family: Times, Times New Roman, serif;" class="font-color">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 0 0 1 1</span>
    </div>
    <div >
        <span style="font-family: Times, Times New Roman, serif;" class="font-color">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ----------------</span>
    </div>
    <div >
        <span style="font-family: Times, Times New Roman, serif;" class="font-color">We count the number of 1s for each bit -&gt; &nbsp;0 0 4 3</span>
    </div>
    <div >
        <span style="font-family: Times, Times New Roman, serif;" class="font-color">Taking modulo 3 we get &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 0 0 1 0</span>
    </div>
    <div >
        <span style="font-family: Times, Times New Roman, serif;" class="font-color">and that's our answer. -&gt; 2</span>
    </div>

</blockquote>

__Second solution is different, and very hard to read/write__. I will not cover this solution. An analysis is found [here](http://zhaohongze.com/wordpress/2013/12/04/leetcode-single-number-ii/): 

> The basic idea is use two integer, __ones and twos__. __Ones__ is used to record the bits only exist once in current iterated number. __Twos__ is used to record the bits only exist twice in all number. If a bit exists up to three times, we should clear it in both ones and twos.

### Code

__my code__

    public int singleNumber(int[] A) {
		int result = 0;
        for (int i = 0; i < 32; i++) {
			int count = 0;
			for (Integer in: A) {
				count += (in & (1 << i)) == 0 ? 0 : 1;
			}
			if (count % 3 != 0) {
				result = result | (1 << i);
			}
		}
		return result;
    }

__a different solution__

    public int singleNumber(int[] A) {
		int ones = 0, twos = 0;
		for (int i = 0; i < A.length; i++) {
			twos = twos | (ones & A[i]);
			ones = ones ^ A[i];

			int common_mask = ~(ones & twos);
			ones &= common_mask;
			twos &= common_mask;
		}
		return ones;
	}
