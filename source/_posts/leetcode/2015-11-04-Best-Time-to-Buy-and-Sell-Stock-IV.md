---
layout: post
title: "[LeetCode 188] Best Time to Buy and Sell Stock IV "
comments: true
category: Leetcode
---

### Question 

[link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/)

<div class="question-content">
              <p></p><p>Say you have an array for which the <i>i</i><sup>th</sup> element is the price of a given stock on day <i>i</i>.</p>

<p>Design an algorithm to find the maximum profit. You may complete at most <b>k</b> transactions.</p>

<p><b>Note:</b><br>
You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).</p>

<p><b>Credits:</b><br>Special thanks to <a href="https://oj.leetcode.com/discuss/user/Freezen">@Freezen</a> for adding this problem and creating all test cases.</p><p></p>
              
                <div id="tags" class="btn btn-xs btn-warning">Show Tags</div>
                <span class="hide">
                  
                  <a class="btn btn-xs btn-primary" href="/tag/dynamic-programming/">Dynamic Programming</a>
                  
                </span>
              
            </div>

### Solution

This question is very difficult. We need to do __DP with 2 DP arrays__, available to read [here](http://blog.csdn.net/linhuanmars/article/details/23236995). 

The 2 arrays' definition as follow:

> global[i][j]=max(local[i][j],global[i-1][j])

> 当前到达第i天可以最多进行j次交易，最好的利润是多少（global[i][j]）
>
> 当前到达第i天，最多可进行j次交易，并且最后一次交易在当天卖出的最好的利润是多少（local[i][j]）

And the formula for calculating local[] is:

> local[i][j]=max(global[i-1][j-1]+max(diff,0),local[i-1][j]+diff)，

> 第一个是全局到i-1天进行j-1次交易，然后加上今天的交易，如果今天是赚钱的话（也就是前面只要j-1次交易，最后一次交易取当前天），
>
> 第二个量则是取local第i-1天j次交易，然后加上今天的差值。

And the final code (by blogger __Code_Ganker__ from the same link) would look like this:

    public int maxProfit(int[] prices) {
        if(prices==null || prices.length==0)
            return 0;
        int[] local = new int[3];
        int[] global = new int[3];
        for(int i=0;i<prices.length-1;i++)
        {
            int diff = prices[i+1]-prices[i];
            for(int j=2;j>=1;j--)
            {
                local[j] = Math.max(global[j-1]+(diff>0?diff:0), local[j]+diff);
                global[j] = Math.max(local[j],global[j]);
            }
        }
        return global[2];
    }
