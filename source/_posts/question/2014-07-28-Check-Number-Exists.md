---
layout: post
title: "[Question] Check If Number Exists"
comments: true
category: Question
tags: [ src ]
---

### Question 

[link](http://tech-queries.blogspot.sg/2011/02/check-if-number-exist.html)

> There is long list of natural numbers. Remove every 2nd no from list in 1st pass. Remove every 3rd no from list in 2nd pass. Find whether Nth natural no will exist after P passes. N and P are inputs.

    Example: N is 15 and p is 3.
    Initial: 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20
    After 1st pass: 1 3 5 7 9 11 13 15 17 19
    After 2nd pass: 1 3 7 9 13 15 19
    After 3rd pass: 1 3 7 13 15 19
    After 4th pass: 1 3 7 13 19

> So we see that 15 exists after 3 passes but vanishes after 4th pass.

### Analysis

We see that in any of the pass __new position will be decreased by no of elements deleted__ between 1 and current position. 

Example: originally number is 15. After 1st pass, it becomes 8th element. After 2nd pass, it becomes 8 - (8 / 3) = 6th element. 

We stop when either P(i-1)/(i+1) is an integer, or when number is smaller than pass. 

### Code

__not written by me__ 

    bool check_posiiton(int n, int p)  
    {  
     int cur = n;  
     int i = 0;  
     while (i <= p)  
     {  
         i++;  
         if (cur%(i+1) == 0)  
         {  
             //Vanishes in this pass  
             return false;  
         }  
         else if (cur < (i+1))  
         {  
             //Number exist denominator is greater than numerator  
             return true;  
         }  
         cur = cur - cur/(i+1);  
     }  
     return true;  
    }  
