---
layout: post
title: "[LeetCode 16] 3Sum Closest"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/3sum-closest/)

<div class="question-content">
            <p></p><p>Given an array <i>S</i> of <i>n</i> integers, find three integers in <i>S</i> such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.</p>

<pre>    For example, given array S = {-1 2 1 -4}, and target = 1.

    The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
</pre><p></p>
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
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

This question is a simplified version of __[LeetCode 15] 3Sum__. The required return is an integer instead of a list. 

This makes life easier because __we do not need to consider duplications__ (think about it, why?). 

### Solution

The code is 3Sum solution without duplication avoidance. 

### My code 

    public class Solution {
        public int threeSumClosest(int[] num, int target) {
            if (num == null || num.length < 3) {
                return 0;
            }
            Arrays.sort(num);
            int len = num.length;
            int ans = num[0] + num[1] + num[2];
            for (int i = 0; i < len; i++) {
                // if (i != 0 && num[i - 1] == num[i]) {
                //     continue;
                // }
                // similar to 3sum question, but without dup avoidance
                int left = i + 1;
                int right = len - 1;
                while (left < right) {
                    int sum = num[i] + num[left] + num[right];
                    // if found triplet that sums to target, return!
                    if (sum == target) {
                        return target;
                    }
                    // then update ans variable - if it's closer to target
                    if (Math.abs(sum - target) < Math.abs(ans - target)) {
                        ans = sum;
                    }
                    // now move either left or right pointer
                    if (sum >  target) {
                        right--;
                    } else {
                        left++;
                    }
                }
            }
            return ans;
        }
    }
