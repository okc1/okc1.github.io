---
layout: post
title: "[Question] Square Count of Matchstick Graph"
comments: true
category: Question

---

### Question 

> 给出下面这个图 设计数据结构和算法求出图中__所有的正方形数量__ (count the number of squares). 

{% img middle /assets/images/matchstick-square-count.jpg %}

### Solution

1. __Pre-processing__: 从每一个点开始存储上下左右四个方向最多延伸到的位置

1. __Main algorithm__: 枚举右下角位置 然后枚举正方形边长 

1. 根据预处理的延伸情况判断是否能够有一个正方形被构造出来 

Total time complexity is O(n^3). 

> 预处理可以O(n^2) 预处理是有递推关系的 
>
> 但是后面枚举的部分，只能O(n^3)
>
> __不能动态规划的原因是__：他给定了一个可以变化的图，这个图上规模为n的图和规模为n-1的图中正方形个数之间不存在递推关系。 

And 一般来说处理矩阵的问题，大部分都是O(n^3)

### Code

