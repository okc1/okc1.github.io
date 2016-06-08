---
layout: post
title: "[LintCode] Longest Increasing Subsequence"
comments: true
category: LintCode

---


### Question 

[link](http://lintcode.com/en/problem/longest-increasing-subsequence/)

<div style="min-height:100px">
    <p>Given a sequence of integers, find the longest increasing subsequence (LIS).</p>
    <p>You code should return the length of the LIS.</p>
    <div class="m-t-lg m-b-lg">
    <b>Example</b>
    <div>
        <p>For [5, 4, 1, 2, 3], the LIS &nbsp;is [1, 2, 3], return 3</p>
        <p>For [4, 2, 4, 5, 3, 7], the LIS is [4, 4, 5, 7], return 4</p>
    </div>
    </div>
</div>

### Analysis 

This is one of the __2 most popular questions of DP__. This is a sequences Dp. The equation isn't difficult. Time complexity of DP solution is O(n^2). 

__There's also a binary search solution__ which the time complexity is O(nlgn). It's very complex, and very hard to explain, but I'll try:

Maintain an array called 'array'. A[i] denotes the tail of sequence for LIS = i. Initially A[0] = first element of the input, then keep inserting elements into this array. It's explained in [this post](http://www.geeksforgeeks.org/longest-monotonically-increasing-subsequence-size-n-log-n/).

I will give an example for the input: 0, 8, 4, 12, 2

>Our strategy determined by the following conditions: 
>
>1. If A[i] is smallest among all end candidates of active lists, we will start new active list of length 1.
>
>2. If A[i] is largest among all end candidates of active lists, we will clone the largest active list, and extend it by A[i].
>
>3. If A[i] is in between, we will find a list with largest end element that is smaller than A[i]. Clone and extend this list by A[i]. We will discard all other lists of same length as that of this modified list.

>A[0] = 0. Case 1. There are no active lists, create one.
>
>array = 0
>
>A[1] = 8. Case 2. Clone and extend.
>
>array = 0, 8
>
>A[2] = 4. Case 3. Clone, extend and discard.
>
>array = 0, 4
>
>A[3] = 12. Case 2. Clone and extend.
>
>array = 0, 4, 12
>
>A[4] = 2. Case 3. Clone, extend and discard.
>
>array = 0, 2, 12
>
>So the LIS is (0, 2, 12) of length 3.

### Code

__DP solution, by me__

    public int longestIncreasingSubsequence(int[] nums) {
        // write your code here
        if (nums == null || nums.length == 0) {
            return 0;
        }
        int len = nums.length;
        int[] dp = new int[len];
        dp[0] = 1;
        for (int i = 1; i < len; i++) {
            dp[i] = 1;
            for (int j = 0; j < i; j++) {
                if (nums[j] <= nums[i]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
        }
        int lis = 1;
        for (Integer seq : dp) {
            lis = Math.max(lis, seq);
        }
        return lis;
    }

__Binary search solution__, C++ code from [this post](http://www.geeksforgeeks.org/longest-monotonically-increasing-subsequence-size-n-log-n/). I don't think I am able code this solution. 

    #include <iostream>
    #include <string.h>
    #include <stdio.h>

    using namespace std;

    #define ARRAY_SIZE(A) sizeof(A)/sizeof(A[0])
    // Binary search (note boundaries in the caller)
    // A[] is ceilIndex in the caller
    int CeilIndex(int A[], int l, int r, int key) {
        int m;

        while( r - l > 1 ) {
            m = l + (r - l)/2;
            (A[m] >= key ? r : l) = m; // ternary expression returns an l-value
        }

        return r;
    }

    int LongestIncreasingSubsequenceLength(int A[], int size) {
        // Add boundary case, when array size is one

        int *tailTable   = new int[size];
        int len; // always points empty slot

        memset(tailTable, 0, sizeof(tailTable[0])*size);

        tailTable[0] = A[0];
        len = 1;
        for( int i = 1; i < size; i++ ) {
            if( A[i] < tailTable[0] )
                // new smallest value
                tailTable[0] = A[i];
            else if( A[i] > tailTable[len-1] )
                // A[i] wants to extend largest subsequence
                tailTable[len++] = A[i];
            else
                // A[i] wants to be current end candidate of an existing subsequence
                // It will replace ceil value in tailTable
                tailTable[CeilIndex(tailTable, -1, len-1, A[i])] = A[i];
        }

        delete[] tailTable;

        return len;
    }

    int main() {
        int A[] = { 2, 5, 3, 7, 11, 8, 10, 13, 6 };
        int n = ARRAY_SIZE(A);

        printf("Length of Longest Increasing Subsequence is %d\n",
                LongestIncreasingSubsequenceLength(A, n));

        return 0;
    }