---
layout: post
title: "[LintCode] Trailing Zeros of Factorial"
description: ""
category: LintCode

---


### Question 

[link](http://www.lintcode.com/en/problem/trailing-zeros/)

> Write an algorithm which computes the number of trailing zeros in n factorial.

> Example: 11! = 39916800, so the out should be 2

### Solution

Note that a trailing zero is produced by 2 * 5.

This question basically is couting the number of factor 5 (because factor 2 is always sufficient). 

### Code

    public long trailingZeros(long n) {
        if (n <= 0) {
            return 0;
        }
        long d = 5;
        long result = 0;
        while (d <= n) {
            result += n / d;
            d *= 5;
        }
        return result;
    }
