---
layout: post
title: "[LeetCode 122] Best Time to Buy and Sell Stock II"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)

<div class="question-content">
            <p></p><p>Say you have an array for which the <i>i</i><sup>th</sup> element is the price of a given stock on day <i>i</i>.</p>

<p>Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="white">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Solution

__This solution is best explained [here](http://jane4532.blogspot.sg/2013/07/best-time-to-buy-and-sell-stock.html)__. 

> 就从左到右轮一遍，遇到递增的都给加起来呗。

### Code

    public int maxProfit(int[] prices) {
        int len = prices.length;
		if (len <= 1) return 0;
		int profit = 0;
		for (int i = 1; i < len; i ++) 
			profit += Math.max(0, prices[i] - prices[i-1]);
		return profit;
    }
