---
layout: post
title: "[Question] Largest palindrome product "
comments: true
category: Question
tags: [ unit test needed ]
---

### Question 

[link](http://projecteuler.net/problem=4)

> The largest palindrome made from the product of two 2-digit numbers is 9009 = 91 × 99. 

> Find the largest palindrome made from the product of two 3-digit numbers. 

### Analysis

We suppose the largest such palindrome will have six digits rather than five, because 143*777 = 111111 is a palindrome. And we can tell that 6-digit base-10 palindrome __must be a multiple of 11__. 

So the question becomes finding the largest palindrome under a million that is a __product of two 3-digit numbers__. 

### Solution

We now declare variable m and n: 

1. step m down from 999 to 100 by 1
1. step n down from 999 to 100 by:
    1. if m is divisible by 11, then step n down by 11
    1. if m is indivisible by 11, then step n down by 1
1. keep track of the largest product found so far: p = r * s
    1. next time when we found such product value (m * n), it must be m <= r. So n have to be really large in order to make the final product larger than p. 
    1. i.e. n >= p/m. 
    1. As larger palindromes are found, the range of n gets more restricted 

[reference](http://stackoverflow.com/a/7198175)

### Code

C++ code from stackoverflow

    int main(void) {
      enum { A=100000, B=10000, C=1000, c=100, b=10, a=1, T=10 };
      int m, n, p, q=111111, r=143, s=777;
      int nDel, nLo, nHi, inner=0, n11=(999/11)*11;

      for (m=999; m>99; --m) {
        nHi = n11;  nDel = 11;
        if (m%11==0) {
          nHi = 999;  nDel = 1;
        }
        nLo = q/m-1;
        if (nLo < m) nLo = m-1;

        for (n=nHi; n>nLo; n -= nDel) {
          ++inner;
          // Check if p = product is a palindrome
          p = m * n;
          if (p%T==p/A && (p/B)%T==(p/b)%T && (p/C)%T==(p/c)%T) {
        q=p; r=m; s=n;
        printf ("%d at %d * %d\n", q, r, s);
        break;          // We're done with this value of m
          }

        }
      }
      printf ("Final result:  %d at %d * %d   inner=%d\n", q, r, s, inner);
      return 0;
    }
