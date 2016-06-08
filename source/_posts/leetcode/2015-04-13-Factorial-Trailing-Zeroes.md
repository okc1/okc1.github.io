---
layout: post
title: "[LeetCode 172] Factorial Trailing Zeroes "
comments: true
category: Leetcode
---

### Question

[link](https://leetcode.com/problems/factorial-trailing-zeroes/)

<div class="question-content">
              <p></p><p>Given an integer <i>n</i>, return the number of trailing zeroes in <i>n</i>!.</p>

<p><b>Note: </b>Your solution should be in logarithmic time complexity.</p>

<p><b>Credits:</b><br>Special thanks to <a href="https://oj.leetcode.com/discuss/user/ts">@ts</a> for adding this problem and creating all test cases.</p><p></p>

                <div id="tags" class="btn btn-xs btn-warning">Show Tags</div>
                <span class="hide">

                  <a class="btn btn-xs btn-primary" href="/tag/math/">Math</a>

                </span>

            </div>

### Analysis

This question I've seen it quite a few time, also. We're basically count the number of factor 5s.

Eg.

> n = 5, count = 1

> n = 6, count = 1

> n = 10, count = 2

> n = 24, count = 4

> n = 25, count = 6

> n = 26, count = 6

### Solution

Please read this post __[[LintCode] Trailing Zeros of Factorial]({% post_url /lintcode/2014-07-02-Trailing-Zero-of-Factorial %})__.

### Code

    public class Solution {
        public int trailingZeroes(int n) {
            if (n < 5) {
                return 0;
            }
            int res = 0;
            long base = 5;
            while (n >= base) {
                res += n / base;
                base *= 5;
            }
            return res;
        }
    }

another pretty good solution:

    public class Solution {
        public int trailingZeroes(int n) {
            int count = 0;
            for (int i = n / 5; i > 0; i = i / 5) {
                count = count + i;
            }
            return count;
        }
    }
