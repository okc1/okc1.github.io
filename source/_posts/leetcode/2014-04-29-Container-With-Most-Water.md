---
layout: post
title: "[LeetCode 11] Container With Most Water"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/container-with-most-water/)

<div class="question-content">
            <p></p><p>Given <i>n</i> non-negative integers <i>a<sub>1</sub></i>, <i>a<sub>2</sub></i>, ..., <i>a<sub>n</sub></i>, where each represents a point at coordinate (<i>i</i>, <i>a<sub>i</sub></i>). <i>n</i> vertical lines are drawn such that the two endpoints of line <i>i</i> is at (<i>i</i>, <i>a<sub>i</sub></i>) and (<i>i</i>, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.
</p>
<p>Note: You may not slant the container.
</p><p></p>
</div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="lime">2</td>
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
		<td bgcolor="lime">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

Assume i and j are 2 points in x-axis where i < j. The container volume is decided by the shorter height among the two. 

Assume i is lower than j, there will be no i < jj < j that makes the area of (i,jj) greater than area of (i,j). __In other words, all (i,jj) is smaller than (i,j) so there's no need to check them__. 

Thus we move i forward by 1. This idea is explained in [this post](http://jane4532.blogspot.sg/2013/05/container-with-most-water-leetcode.html). 

### Solution

__Two-pointer scan__. And always move the shorter board index (if we consider it to be a rectangle bucket), as explained in [this post](http://fisherlei.blogspot.sg/2013/01/leetcode-container-with-most-water.html).

### My code 

    public class Solution {
        public int maxArea(int[] height) {
            if (height == null || height.length <= 1) {
                return 0;
            }
            int left = 0;
            int right = height.length - 1;
            int area = 0;
            // start calculating area and shrinking the distance 
            // between left and right pointer
            while (left < right) {
                area = Math.max(area, (right - left) 
                    * Math.min(height[left], height[right]));
                if (height[left] < height[right]) {
                    left++;
                } else {
                    right--;
                }
            }
            return area;
        }
    }
