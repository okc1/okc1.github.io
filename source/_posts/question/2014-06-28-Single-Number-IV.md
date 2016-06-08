---
layout: post
title: "[Question] Single Number IV"
comments: true
category: Question
tags: [ unit test needed ]
---

### Question 

[link](http://www.geeksforgeeks.org/find-the-two-repeating-elements-in-a-given-array/)

> You are given an array of n+2 elements. All elements of the array are in range 1 to n. And all elements occur once except two numbers which occur twice. Find the two repeating numbers.

### Solution

__Solution 1__: User count array. O(n) time and O(n) space. Not efficient enough. 

__Solution 2__: Calculate sum of x,y and product of x,y. O(n) time and O(1) space, but there's risk of overflow. 

__Solution 3__: XOR. Add number 1 to N to the array, and this becomes Single Number III. O(n) time and O(1) space. 

There is also a __solution 4__: Use array elements as index. This is the same method as used in __[LeetCode 41] First Missing Positive__. 

### Code

C++ Code from GFG

    void printRepeating(int arr[], int size)
    {
      int xor = arr[0]; /* Will hold xor of all elements */
      int set_bit_no;  /* Will have only single set bit of xor */
      int i;
      int n = size - 2;
      int x = 0, y = 0;

      /* Get the xor of all elements in arr[] and {1, 2 .. n} */
      for(i = 1; i < size; i++)
        xor ^= arr[i];
      for(i = 1; i <= n; i++)
        xor ^= i;

      /* Get the rightmost set bit in set_bit_no */
      set_bit_no = xor & ~(xor-1);

      /* Now divide elements in two sets by comparing rightmost set
       bit of xor with bit at same position in each element. */
      for(i = 0; i < size; i++)
      {
        if(arr[i] & set_bit_no)
          x = x ^ arr[i]; /*XOR of first set in arr[] */
        else
          y = y ^ arr[i]; /*XOR of second set in arr[] */
      }
      for(i = 1; i <= n; i++)
      {
        if(i & set_bit_no)
          x = x ^ i; /*XOR of first set in arr[] and {1, 2, ...n }*/
        else
          y = y ^ i; /*XOR of second set in arr[] and {1, 2, ...n } */
      }

      printf("\n The two repeating elements are %d & %d ", x, y);
    }     


    int main()
    {
      int arr[] = {4, 2, 4, 5, 2, 3, 1};
      int arr_size = sizeof(arr)/sizeof(arr[0]);  
      printRepeating(arr, arr_size);
      getchar();
      return 0;
    }