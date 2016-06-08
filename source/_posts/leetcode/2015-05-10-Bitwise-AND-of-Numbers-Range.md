---
layout: post
title: "[LeetCode 201] Bitwise AND of Numbers Range "
comments: true
category: Leetcode
---

### Question 

[link](https://leetcode.com/problems/bitwise-and-of-numbers-range/)

<div class="question-content">
              <p></p><p>Given a range [m, n] where 0 &lt;= m &lt;= n &lt;= 2147483647, return the bitwise AND of all numbers in this range, inclusive.</p>

<p>
For example, given the range [5, 7], you should return 4.
</p>

<p><b>Credits:</b><br>Special thanks to <a href="https://leetcode.com/discuss/user/amrsaqr">@amrsaqr</a> for adding this problem and creating all test cases.</p><p></p>
              
                <div id="tags" class="btn btn-xs btn-warning">Show Tags</div>
                <span class="hide">
                  
                  <a class="btn btn-xs btn-primary" href="/tag/bit-manipulation/">Bit Manipulation</a>
                  
                </span>
              
            </div>

### Analysis

This is a pretty interesting mathematics question. Now we take 2 numbers as example: 

> Num1: 110010
>
> Num2: 110111
>
> Result: 110000

And:

> Num1: 0110
>
> Num2: 1100
>
> Result: 0

Note that: 

1. if the first '1' bit of the 2 numbers are at different position, the answer should simply be 0.

1. if have same position, then the result would be the continous sequence of 1s, followed by all 0s. 

### Solution

The 2 best solutions is very well presented by [Grandyang](http://www.cnblogs.com/grandyang/p/4431646.html) using bit shifting and masking. Please refer to code 1 and code 2 below. 

I found a third solution at [programcreek](http://www.programcreek.com/2014/04/leetcode-bitwise-and-of-numbers-range-java/), which makes use of the fact that m is smaller than n. 

### Code

code 1

    class Solution {
    public:
        int rangeBitwiseAnd(int m, int n) {
            int d = INT_MAX;
            while ((m & d) != (n & d)) {
                d <<= 1;
            }
            return m & d;
        }
    };

code 2

    class Solution {
    public:
        int rangeBitwiseAnd(int m, int n) {
            int i = 0;
            while (m != n) {
                m >>= 1;
                n >>= 1;
                ++i;
            }
            return (m << i);
        }
    };

code 3

    public int rangeBitwiseAnd(int m, int n) {
         while (n > m) {
              n = n & n - 1;
         }
         return m & n;
    }
