---
layout: post
title: "[LeetCode 190] Reverse Bits "
comments: true
category: Leetcode
---

### Question 

[link](https://leetcode.com/problems/reverse-bits/)

<div class="question-content">
              <p></p><p>Reverse bits of a given 32 bits unsigned integer.</p>

<p>For example, given input 43261596 (represented in binary as <b>00000010100101000001111010011100</b>), return 964176192 (represented in binary as <b>00111001011110000010100101000000</b>).</p>

<p>
<b>Follow up</b>:<br>
If this function is called many times, how would you optimize it?
</p>

<p>Related problem: <a href="/problems/reverse-integer/">Reverse Integer</a></p>

<p><b>Credits:</b><br>Special thanks to <a href="https://oj.leetcode.com/discuss/user/ts">@ts</a> for adding this problem and creating all test cases.</p><p></p>
              
                <div id="tags" class="btn btn-xs btn-warning">Show Tags</div>
                <span class="hide">
                  
                  <a class="btn btn-xs btn-primary" href="/tag/bit-manipulation/">Bit Manipulation</a>
                  
                </span>
              
            </div>

### Analysis

This question is standard bit manipulation. We essentially get bits one by one from n, and append it to the result. 

However, the question ask how to optimize it, to improve its performance. Em, that's interesting. 

### Solution

First code is the standard solution. 

I found another interesting solution from [programcreek](http://www.programcreek.com/2014/03/leetcode-reverse-bits-java/), which uses "swap bits" method. I've never seen this before, so I posted his solution below. 

But is it really a faster solution? 

Finally, I found something in [书影 博客](http://bookshadow.com/weblog/2015/03/08/leetcode-reverse-bits/), quoted as below: 

> 以4位为单位执行反转，将0x0至0xF的反转结果预存在一个长度为16的数组中，反转时直接查询即可。

Thus this is the best solution for performance. 

### Code

My code

    public class Solution {
        // you need treat n as an unsigned value
        public int reverseBits(int n) {
            int result = 0;
            for (int i = 0; i < 32; i++) {
                int last = n & 1;
                n >>= 1;
                result <<= 1;
                result = result | last;
            }
            return result;
        }
    }

"swap bits"

    public int reverseBits(int n) {
        for (int i = 0; i < 16; i++) {
            n = swapBits(n, i, 32 - i - 1);
        }

        return n;
    }

    public int swapBits(int n, int i, int j) {
        int a = (n >> i) & 1;
        int b = (n >> j) & 1;

        if ((a ^ b) != 0) {
            return n ^= (1 << i) | (1 << j);
        }

        return n;
    }

Best solution: 

    char tb[16] = {0,8,4,12,2,10,6,14,1,9,5,13,3,11,7,15};

    uint32_t reverseBits(uint32_t n) {
            int curr = 0;
            uint32_t ret = 0;
            uint32_t msk = 0xF;
            for(int i = 0; i < 8; i++) {
                ret = ret << 4;
                curr = msk&n;
                ret |= tb[curr];
                n = n >> 4;
            }
            return ret;
    }
