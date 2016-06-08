---
layout: post
title: "[Facebook] Generate number with Given probability "
comments: true
category: q-facebook

---

### Question 

[link](http://blog.sina.com.cn/s/blog_b9285de20101h463.html)

> 给定一个随机函数可以按照0.5的概率返回true。

> 要求实现一个函数随机返回任意概率的true。

### Solution 

Eg. 0.25 true, then should be: 

1. generate once. If false, return false, else...

1. generate again, directly return.

So, always return result for the possibility larger than 0.5. This recursion might go on forever. 

Read code below. 

### Code

not my code

    boolean RNGwithGivenProb(double p, boolean expected)
    {
       if(p < 0.5)
           return RNGwithGivenProb(1 - p, !expected);  
       if(RNG() == expected)
           return expected;
       else
           return RNGwithGivenProb((p - 0.5) * 2, expected);
    }

    boolean RNG()
    {
       return T/F with 0.5 probability.
    }
