---
layout: post
title: "[Question] Maximum square sub-matrix with all 1s "
comments: true
category: Question
tags: [ src ]
---

### Question

[link](http://www.geeksforgeeks.org/maximum-size-sub-matrix-with-all-1s-in-a-binary-matrix/)

> Given a binary matrix, find out the maximum size square sub-matrix with all 1s. For example, consider the below binary matrix.

       0  1  1  0  1 
       1  1  0  1  0 
       0  1  1  1  0
       1  1  1  1  0
       1  1  1  1  1
       0  0  0  0  0

> The maximum square sub-matrix with all set bits is size 9. Note we only find __square__, not rectangles! (this makes it much easier)

### Solution

Since __square only__, we can use DP. [Quoted answer](http://www.geeksforgeeks.org/maximum-size-sub-matrix-with-all-1s-in-a-binary-matrix/) below: 

> Let the given binary matrix be M[R][C]. The idea of the algorithm is to construct an auxiliary size matrix S[][] in which each entry S[i][j] represents size of the square sub-matrix with all 1s including M[i][j] where M[i][j] is the rightmost and bottommost entry in sub-matrix.

> 1. Construct a sum matrix S[R][C] for the given M[R][C].
>
>   1. Copy first row and first columns as it is from M[][] to S[][]
>
>   1. For other entries, use following expressions to construct S[][]

             If M[i][j] is 1 then
                S[i][j] = min(S[i][j-1], S[i-1][j], S[i-1][j-1]) + 1
             Else /*If M[i][j] is 0*/
                S[i][j] = 0
