---
layout: post
title: "[Question] Subarray with Sum Closest"
comments: true
category: Question
tags: [ unit test needed ]
---

### Question 

[link](http://www.geeksforgeeks.org/minimum-length-subarray-sum-greater-given-value/)

> Given an array of integers and a number x, find the smallest subarray with sum greater than the given value.
>
> Eg. input = (1, 4, 45, 6, 0, 19), 51, output (4, 45, 6)

### Solution

__Solution 1 (the better one)__ is based on another question __Subarray with 0 Sum__. We calculate the 前缀和 of every number. Takes O(n) time. 

If all input are positive, there can be a __Solution 2__ which is based on another question __Subarray with Particular Sum__. The sliding window search. It's O(n) time as well. 

### Code

__Solution 2__ (for positive input) 

    int smallestSubWithSum(int arr[], int n, int x) {
        //  Initilize length of smallest subarray as n+1
         int min_len = n + 1;

         // Pick every element as starting point
         for (int start=0; start<n; start++)
         {
              // Initialize sum starting with current start
              int curr_sum = arr[start];

              // If first element itself is greater
              if (curr_sum > x) return 1;

              // Try different ending points for curremt start
              for (int end=start+1; end<n; end++)
              {
                  // add last element to current sum
                  curr_sum += arr[end];

                  // If sum becomes more than x and length of
                  // this subarray is smaller than current smallest
                  // length, update the smallest length (or result)
                  if (curr_sum > x && (end - start + 1) < min_len)
                     min_len = (end - start + 1);
              }
         }
         return min_len;
    }
