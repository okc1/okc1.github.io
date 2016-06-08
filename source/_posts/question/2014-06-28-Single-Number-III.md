---
layout: post
title: "[Question] Single Number III"
comments: true
category: Question
tags: [ unit test needed ]
---


### Question 

[link](http://www.geeksforgeeks.org/find-two-non-repeating-elements-in-an-array-of-repeating-elements/)

> In an array, all numbers in the array repeat twice except two numbers, which repeat only once. 

> Assume all the numbers are placed randomly. Find the 2 numbers. 

### Analysis 

The main idea of the solution is how to remove repeated elements. It's definitely __using XOR__. 

We need to try solve this problem like we did in 'Single number 1' but how? We can divide the array into 2 part, each part containing 1 non-repeating number. 

The difficulty and the trick, is how do we divide?

### Solution

1. xor = arr[0]^arr[1]^arr[2].....arr[n-1]

1. We can extract the rightmost set bit of any number n by taking ( n & ~(n-1))

1. We take any set bit of xor and __divide the elements of the array in two sets__ – one set of elements with same bit set and other set with same bit not set. 

    By doing so, we will get x in one set and y in another set. 

### Code

C++ Code from GFG

    /* This finction sets the values of *x and *y to nonr-epeating
     elements in an array arr[] of size n*/
    void get2NonRepeatingNos(int arr[], int n, int *x, int *y)
    {
      int xor = arr[0]; /* Will hold xor of all elements */
      int set_bit_no;  /* Will have only single set bit of xor */
      int i;
      *x = 0;
      *y = 0;

      /* Get the xor of all elements */
      for(i = 1; i < n; i++)
       xor ^= arr[i];

      /* Get the rightmost set bit in set_bit_no */
      set_bit_no = xor & ~(xor-1);

      /* Now divide elements in two sets by comparing rightmost set
       bit of xor with bit at same position in each element. */
      for(i = 0; i < n; i++)
      {
        if(arr[i] & set_bit_no)
         *x = *x ^ arr[i]; /*XOR of first set */
        else
         *y = *y ^ arr[i]; /*XOR of second set*/
      }
    }

    /* Driver program to test above function */
    int main()
    {
      int arr[] = {2, 3, 7, 9, 11, 2, 3, 11};
      int *x = (int *)malloc(sizeof(int));
      int *y = (int *)malloc(sizeof(int));
      get2NonRepeatingNos(arr, 8, x, y);
      printf("The non-repeating elements are %d and %d", *x, *y);
      getchar();
    }
