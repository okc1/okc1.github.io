---
layout: post
title: "[Google] Orthogonal Traverse the Map (`)"
comments: true
category: q-google

---

### Question 

[link](http://www.itint5.com/oj/#22)

> 有一个n*m（n和m都不超过50）的棋盘，有k个目标格子需要访问。需要访问的格子的横纵坐标存放在数组x[]和y[]中(0<=x[i]<n, 0<=y[i]<m)。

> 遍历的规则为：
>
> 每一步只能从一个目标格子水平或者竖直跳跃移动到另一个目标格子。
>
> 连续的两步必须形成直角。即如果前一步是水平移动，那么下一步只能竖直移动。
>
> 问是否存在一种遍历顺序，使得每个目标格子有且仅被访问一次。

> 样例：k=8, x=[0, 0, 0, 0, 2, 2, 4, 4], y=[0, 2, 4, 6, 4, 6, 2, 4],对应于下图中A, B, C, D, F, E, G, H 8个目标格子，存在满足条件的遍历A->D->E->F->C->B->G->H。

{% img middle /assets/images/orthogonal-map.jpg %}

### Solution

> n,m的棋盘，[建一个包含n+m个顶点的图G](http://www.itint5.com/discuss/22/%E7%9B%B4%E8%A7%92%E8%B7%AF%E7%BA%BF%E9%81%8D%E5%8E%86%E6%A3%8B%E7%9B%98)（为了方便说明，类似二分图将其分为两列，左边n个顶点，右边m个顶点，分别代表n行和n列）。

> 对于目标格子(i,j)，左边第i个顶点和右边第j个顶点连一条边。最后的问题其实就是问转换之后的图G是否存在欧拉欧拉回路或者欧拉路径。
