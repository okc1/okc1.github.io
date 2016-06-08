---
layout: post
title: "[LeetCode 152] Maximum Product Subarray "
comments: true
category: Leetcode
---

### Question 

[link](https://leetcode.com/problems/maximum-product-subarray/)

<div class="question-content">
              <p></p><p>
Find the contiguous subarray within an array (containing at least one number) which has the largest product.
</p>

<p>
For example, given the array <code>[2,3,-2,4]</code>,<br>
the contiguous subarray <code>[2,3]</code> has the largest product = <code>6</code>.
</p><p></p>
              
                <div id="tags" class="btn btn-xs btn-warning">Show Tags</div>
                <span class="hide">
                  
                  <a class="btn btn-xs btn-primary" href="/tag/array/">Array</a>
                  
                  <a class="btn btn-xs btn-primary" href="/tag/dynamic-programming/">Dynamic Programming</a>
                  
                </span>
              
            </div>

### Analysis

__This is a pretty difficult question__. It's hard to write bug-free solution if you have never practised before. 

So the first idea that comes to me is the case of array element = 0. Why this case? cuz the maximum subarray MUST NOT CONTAIN 0 unless the input is like {-1, 0, -1}. So we could divide array from 0s and calculate max sum seperately. This idea is good, though a little difficult in coding. Read it [here](http://www.geeksforgeeks.org/maximum-product-subarray/) or [here](https://shepherdyuan.wordpress.com/2014/07/23/linkedin-maximum-sumproduct-subarray/). 

### Solution

After a bit exploration, I found a must easier apporach, thanks to [code ganker](http://blog.csdn.net/linhuanmars/article/details/39537283) and [Yu](http://yucoding.blogspot.sg/2014/10/leetcode-quesion-maximum-product.html). The idea is to simply ALWAYS CALCULATE preMax and preMin by using MAX/MIN(Val1, Val2, Val3) method.  

### My Code

    public class Solution {
        public int maxProduct(int[] A) {
            if (A == null || A.length == 0) {
                return 0;
            } else if (A.length == 1) {
                return A[0];
            }

            int preMax = A[0];
            int preMin = A[0];
            int max = A[0];

            for (int i = 1; i < A.length; i++) {
                int temp = preMin;
                preMin = Math.min(Math.min(preMin * A[i], preMax * A[i]), A[i]);
                preMax = Math.max(Math.max(temp * A[i], preMax * A[i]), A[i]);
                max = Math.max(max, preMax);
            }

            return max;
        }
    }
