---
layout: post
title: "[LeetCode 123] Best Time to Buy and Sell Stock III"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/)

<div class="question-content">
            <p></p><p>Say you have an array for which the <i>i</i><sup>th</sup> element is the price of a given stock on day <i>i</i>.</p>

<p>Design an algorithm to find the maximum profit. You may complete at most <i>two</i> transactions.</p>

<p><b>Note:</b><br>
You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is much harder to solve then previous 2 question combined__. 

### Solution

The best solution is explained in [this blog](http://rleetcode.blogspot.sg/2014/02/best-time-to-buy-and-sell-stock-iii-java.html). 

> we can just dived the whole prices array at every point, try to calculate max profit from left and from right respectively...

> However, there are many repeat calculations. So we can apply DP to record max profits for each left side and right side. then add them together at each point.

A detailed illustration with examples can be found [here](http://yucoding.blogspot.sg/2012/12/leetcode-question-10-best-time-to-buy.html). 

However, the coding part is slightly difficult at least for me. __I made a terrible mistake with the variable 'leftMin' and 'rightMax'__. I declared it as __'rightMin'__ instead, and then the program logic is wrong. We should avoid this kind of mistakes. 

### Code

    public int maxProfit(int[] prices) {
        int len = prices.length;
        if (len == 0) return 0;
        int leftMin = Integer.MAX_VALUE, rightMax = Integer.MIN_VALUE;
        int leftPro[] = new int[len], rightPro[] = new int[len];
        for (int j = 0; j <= len - 1; j ++) {
            leftMin = Math.min(leftMin, prices[j]);
            if (j == 0) leftPro[0] = 0;
            else leftPro[j] = Math.max(leftPro[j-1], prices[j] - leftMin);
        }
        for (int k = len - 1; k >= 0; k --) {
            rightMax = Math.max(rightMax, prices[k]);
            if (k == len - 1) rightPro[len-1] = 0;
            else rightPro[k] = Math.max(rightPro[k+1], rightMax - prices[k]);
        }
        int totalPro = 0;
        for (int i = 0; i < len; i ++) {
            totalPro = Math.max(totalPro, leftPro[i] + rightPro[i]);
        }
        return totalPro;
    }
