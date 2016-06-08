---
layout: post
title: "[LeetCode 121] Best Time to Buy and Sell Stock"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/best-time-to-buy-and-sell-stock/)

<div class="question-content">
            <p></p><p>Say you have an array for which the <i>i</i><sup>th</sup> element is the price of a given stock on day <i>i</i>.</p>

<p>If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a question from a MIT course__, [Hacking a Google Interview](http://courses.csail.mit.edu/iap/interview/materials.php). 

I did not solve it, but it's actually very simple to do. 

### Solution

The solution is explained [here](http://leetcode.com/2010/11/best-time-to-buy-and-sell-stock.html): 

> To solve this problem efficiently, you would need to track the minimum value’s index. As you traverse, update the minimum value’s index when a new minimum is met. Then, compare the difference of the current element with the minimum value. Save the buy and sell time when the difference exceeds our maximum difference (also update the maximum difference).

> Time is O(N)

### Code

    public int maxProfit(int[] prices) {
		int len = prices.length;
		if (len <= 1) return 0;
		int min = prices[0];
		int max = Integer.MIN_VALUE;
		for (int i = 1; i < len; i ++) {
			max = Math.max(max, prices[i] - min);
			min = Math.min(min, prices[i]);
		}
		return Math.max(max, 0);
    }
