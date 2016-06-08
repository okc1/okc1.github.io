---
layout: post
title: "[Question] 编程之美 NIM 一排石头的游戏 "
comments: true
category: Question

---

### Question 

[link](http://blog.csdn.net/starcuan/article/details/20546993)

> N块石头排成一行，两个玩家依次取石头，每个玩家可以取其中任意一块或者相邻的两块，最后能将剩下的石头一次取光的玩家获胜。


### Solution

1. when n = 1, first move wins
1. when n = 2, first move wins
1. when n = 3, first move removes middle stone, wins
1. when n = 4, first move removes 2 stones from middle, wins
1. when n = 5, first move removes middle stone, which leaves 2 piles of stones of count 2. First move wins.

So to conclude the above, we will have: 

> 先取者只要取中间的元素，N为奇数取中间一个，偶数取中间两个，将石头分为两部分，然后无论第二个人怎么取，先取者只要在另一部分的同样位置取走同样多的石头，则最后先取者必胜

Quoted from [王川的私房菜
](http://blog.csdn.net/starcuan/article/details/20546993). 
