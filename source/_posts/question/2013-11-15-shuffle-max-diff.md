---
layout: post
title: "[Question] Shuffle and Get Max Difference "
comments: true
category: Question
tags: [  ]
---

# Question

[link](http://stackoverflow.com/questions/23205277/max-absolute-sum-in-a-array)

> Given an array with four integers A, B, C, D, shuffle them in some order (there are 24 shuffles). 

> ... Get the best shuffle such that

> F(S) = abs(s[0]-s[1]) + abs(s[1]-s[2])+ abs(s[2]-s[3])
is maximum

> For example

    A=5, B= 3, C=-1, D =5
    s[0]=5, s[1]=-1, s[2]= 5, s[3] =3

> will give F[s] =14 as max diff

# Solution

Referring to [this execellent answer](http://stackoverflow.com/a/23205616):

1. sort input and we get 4 number from min to max: A B C D
1. swap A and B - B A C D
1. swap C and D - B A D C
1. swap head and tail - C A D B

Finally you got CADB or BDAC.
