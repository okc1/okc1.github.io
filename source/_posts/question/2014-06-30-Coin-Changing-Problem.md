---
layout: post
title: "[Question] Coin Change Problem"
comments: true
category: Question
tags: [ unit test needed ]
---


### Question 

[link](http://www.geeksforgeeks.org/dynamic-programming-set-7-coin-change/)

> Given a value N, if we want to make change for N cents, and we have infinite supply of each of S = { S1, S2, .. , Sm} valued coins, how many ways can we make the change? The order of coins doesn’t matter.

> For example, for N = 4 and S = {1,2,3}, there are four solutions: {1,1,1,1},{1,1,2},{2,2},{1,3}. So output should be 4. For N = 10 and S = {2, 5, 3, 6}, there are five solutions: {2,2,2,2,2}, {2,2,3,3}, {2,2,6}, {2,3,5} and {5,5}. So the output should be 5.

### Analysis

I did this question before, it's not a DFS search question, because question only asks the total number of ways. 

So what method do we use? Remember the 4 types of DP?

>1. Input cannot sort
>
>1. Find minimum/maximum result
>
>1. Check the feasibility
>
>1. Count all possible solutions

So, this is a DP question! 

### Solution

The solutions in in two parts: 

1. Solutions that do not contain mth coin (or Sm).
2. Solutions that contain at least one Sm.

Using m to denote the types of coin used, and n denote the total value, the equation is: 

> count( S, m, n ) = count( S, m - 1, n ) + count( S, m, n-S[m-1] )

__Solution one is using recursion__. It's not good because of a lot of repeated calculation. But the code is extremely easy to write: 

    int count( int S[], int m, int n ) {
        // If n is 0 then there is 1 solution (do not include any coin)
        if (n == 0)
            return 1;
        // If n is less than 0 then no solution exists
        if (n < 0)
            return 0;
        // If there are no coins and n is greater than 0, then no solution exist
        if (m <=0 && n >= 1)
            return 0;
        // count is sum of solutions (i) including S[m-1] (ii) excluding S[m-1]
        return count( S, m - 1, n ) + count( S, m, n-S[m-1] );
    }

__Solution two is DP__, it's a little hard to write actually. Do it carefully. 

### Code

C++ code not written by me: 

    int count( int S[], int m, int n ) {
        int i, j, x, y;

        // We need n+1 rows as the table is consturcted in bottom up manner using 
        // the base case 0 value case (n = 0)
        int table[n+1][m];

        // Fill the enteries for 0 value case (n = 0)
        for (i=0; i<m; i++)
            table[0][i] = 1;

        // Fill rest of the table enteries in bottom up manner  
        for (i = 1; i < n+1; i++)
        {
            for (j = 0; j < m; j++)
            {
                // Count of solutions including S[j]
                x = (i-S[j] >= 0)? table[i - S[j]][j]: 0;

                // Count of solutions excluding S[j]
                y = (j >= 1)? table[i][j-1]: 0;

                // total count
                table[i][j] = x + y;
            }
        }
        return table[n][m-1];
    }
