---
layout: post
title: "[Question] Make a fair coin from a biased coin"
comments: true
category: Question

---


### Question 

[link](http://www.geeksforgeeks.org/print-0-and-1-with-50-probability/)

> You are given a function foo() that represents a biased coin. When foo() is called, it returns 0 with 60% probability, and 1 with 40% probability. Write a new function that returns 0 and 1 with 50% probability each. Your function should use only foo(), no other library method. 

### Analysis

(0, 1): The probability to get 0 followed by 1 from two calls of foo() = 0.6 * 0.4 = 0.24

(1, 0): The probability to get 1 followed by 0 from two calls of foo() = 0.4 * 0.6 = 0.24

### Solution

Toss twice. If get (0, 0) or (1, 1), discard. Otherwise, return 0 or 1 for the 2 different cases. 

### Code

    int my_fun() {
        int val1 = foo();
        int val2 = foo();
        if (val1 == 0 && val2 == 1)
            return 0;   // Will reach here with 0.24 probability
        if (val1 == 1 && val2 == 0)
            return 1;   // Will reach here with 0.24 probability
        return my_fun();
    }
