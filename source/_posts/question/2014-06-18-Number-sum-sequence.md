---
layout: post
title: "[Question] Number Sum Sequence"
comments: true
category: Question
tags: [ unit test needed ]
---


### Question 

[link](http://bbs.csdn.net/topics/390332954)

>定义一个数字有以下的特征, 它可以被分成几个部分,而前面的部分相加起来的和是后面的部分.举例来说 
>
>1235813,       1+2=3; 2+3=5;3+5=8; 5+8=13;
>
>112112224,     112+112=224;
>
>1981100,       19+81=100;
>
>122436,        12+24=36;
>
>1299111210,    12+99=111,99+111=210;
>
>要求写出一个函数,输入一个数字,判断这个数字是不是要求的这个数。

### Analysis

__This is a difficult DFS search question__. Basic idea from [this blog](http://bbs.csdn.net/topics/390332954): 

> 取前i位为a1,第i+1到j位为a2,检测n是否由a1和a2生成的序列组成。
>
> 时间复杂度为O(n^3)（或O(n^2)). 

### Code

The code is surprisingly very short. 

I have yet to prove whether this code works. 

    def isLegal(n, i, j):
        """取前i位为a1,第i+1到j位为a2,检测n是否由a1和a2生成的序列组成。"""
        nextDigit = j
        a1 = int(n[:i])
        a2 = int(n[i:j])
        while nextDigit<len(n): # n还有数字可用
            a2, a1 = a1+a2, a2
            s2 = str(a2)
            if n.startswith(s2, nextDigit): #从n的第nextDigit位开始，与s2比较
                nextDigit += len(s2)
            else:
                return False
        return True

    def test(n):
        for i in range(1, len(n)-1):
            for j in range(i+1, len(n)-1):
                if isLegal(n, i, j):
                    return True
        return False
