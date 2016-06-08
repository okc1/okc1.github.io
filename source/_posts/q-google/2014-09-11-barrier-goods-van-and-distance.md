---
layout: post
title: "[Google] Barrier, Goods Van and Distance "
comments: true
category: q-google

---

### Question

[link](http://www.mitbbs.com/article_t1/JobHunting/32631467_0_1.html)

> 2d array ＊代表障碍物 ＃代表货物 空白就是正常的路 

> 问如何找到一个点为出发点 能实现总共取货路径最短？ 每次只能拿一个货物，遇到障碍需要绕开，拿到以后要放回出发点，然后再取另一个. 

    ＊＊＊＊＊＊＊＊＊＊
    ＊  #           ＊
    ＊  ＊＊＊  ＊   ＊
    ＊              ＊
    ＊     ＊＊   ＊ ＊
    ＊  #    # # ＊＊＊
    ＊＊＊＊＊＊＊＊＊＊

### Solution

This looks like a very difficult question, especially during a phone interview. 

__The 10th floor gives the best solution__: 

> __BFS from every box__. in each box, a non-blocking cell (include box position, but exclude hazard position) will have a weight value, stand for the distance to the box. 

> after bfs from all the boxes, each cell will have k weight, k is the number of boxes. sum all the weight in each cell, and find the cell with smallest sum of weight. 

> One problem of this solution may lead to a cell of a box. We can then sort the cell by sum of weight and find the first position that is not a box. 

> complexity O(k*n^2)

Suggested at [this post](http://www.mitbbs.com/article_t/JobHunting/32602449.html), we can also use __A* search (with heuristic function)__ to solve. 

### Code

__not written__
