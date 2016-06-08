---
layout: post
title: "[Question] Ways of Dice Throw"
comments: true
category: Question

---

### Question 

[link](http://www.geeksforgeeks.org/dice-throw-problem/)

> Given n dice each with m faces, numbered from 1 to m, find the number of ways to get sum X. X is the summation of values on each face when all the dice are thrown. 

### Solution

__DP__

> Sum(m, n, X) = Sum(m, n - 1, X - 1) + 
>
>                Sum(m, n - 1, X - 2) +
>
>                .................... + 
>
>                Sum(m, n - 1, X - m)

So we can have dp(n)(X) and for each, iterate m time. Total time is O(m * n * X). 

### Code

__not written by me__.

	int findWays(int m, int n, int x)
	{
	    // Create a table to store results of subproblems.  One extra 
	    // row and column are used for simpilicity (Number of dice
	    // is directly used as row index and sum is directly used
	    // as column index).  The entries in 0th row and 0th column
	    // are never used.
	    int table[n + 1][x + 1];
	    memset(table, 0, sizeof(table)); // Initialize all entries as 0
	 
	    // Table entries for only one dice
	    for (int j = 1; j <= m && j <= x; j++)
	        table[1][j] = 1;
	 
	    // Fill rest of the entries in table using recursive relation
	    // i: number of dice, j: sum
	    for (int i = 2; i <= n; i++)
	        for (int j = 1; j <= x; j++)
	            for (int k = 1; k <= m && k < j; k++)
	                table[i][j] += table[i-1][j-k];
	 
	    /* Uncomment these lines to see content of table
	    for (int i = 0; i <= n; i++)
	    {
	      for (int j = 0; j <= x; j++)
	        cout << table[i][j] << " ";
	      cout << endl;
	    } */
	    return table[n][x];
	}
