---
layout: post
title: "[LeetCode 191] Number of 1 Bits "
comments: true
category: Leetcode
---

### Question 

[link](https://leetcode.com/problems/number-of-1-bits/)

<div class="question-content">
              <p></p><p>Write a function that takes an unsigned integer and returns the number of ’1' bits it has (also known as the <a href="http://en.wikipedia.org/wiki/Hamming_weight">Hamming weight</a>).</p>

<p>For example, the 32-bit integer ’11' has binary representation <code>00000000000000000000000000001011</code>, so the function should return 3.</p>

<p><b>Credits:</b><br>Special thanks to <a href="https://oj.leetcode.com/discuss/user/ts">@ts</a> for adding this problem and creating all test cases.</p><p></p>
              
                <div id="tags" class="btn btn-xs btn-warning">Show Tags</div>
                <span class="hide">
                  
                  <a class="btn btn-xs btn-primary" href="/tag/bit-manipulation/">Bit Manipulation</a>
                  
                </span>
              
            </div>

### Analysis

In order to remove the last '1' bit, we use this operation: 

    n = n & (n - 1);

### Solution

Just remove all the '1' bits. 

### Code

    public class Solution {
        public int hammingWeight(int n) {
            int count = 0;
            while (n != 0) {
                n = n & (n - 1);
                count++;
            }
            return count;
        }
    }
