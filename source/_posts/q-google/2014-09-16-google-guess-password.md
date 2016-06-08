---
layout: post
title: "[Google] Guess Password "
comments: true
category: q-google

---

### Question 

[link](http://www.mitbbs.com/article_t/JobHunting/32658281.html)

> 给你一个password 假定6位

> 有个function, 每call一次就给你一个triplet 是password 里的随即三位(order不变)。比如google, 可能返回: ggl, goe, oog, ool...

> 问如何最有效破译这个密码? 

### Solution

This is just a rough idea suggested by Level 6 of [this post](http://www.mitbbs.com/article_t/JobHunting/32658281.html). 

> 六位密码随机给三位，应该有C(6, 3) = 20个bucket。 

> 如果密码是abcdef，那么以a开头的bucket应该是 C(5, 2) = 10个。以b开头的buckt应该是C(4, 2) = 6个，以c开头的是3个，以d开头的是1个.... from this, we know the probability of the occurrance of each letter. 

In this case, we generate many triplets, and calculate based on their frequencies. However, the guy also wrote about this condition: 

> 如果abcd中间有相同(there are same letters in the 6-char password)，那么就会出现以a开头的是11个（abca)，13个(abad)，14个(abaa)，16个(aacd)，17个(aaca),19个(aaad)或者20个(aaaa). 

> 思路是比较清楚，不过算法还要想想。

### Code

__not written__
