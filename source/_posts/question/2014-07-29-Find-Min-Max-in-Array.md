---
layout: post
title: "[Question] Find Min & Max in an Array Using Minimum Comparisons"
comments: true
category: Question

---

### Question 

[link](http://www.programcreek.com/2014/02/find-min-max-in-an-array-using-minimum-comparisons/)

> Given an array of integers find the maximum and minimum elements by using minimum comparisons. 

### Solution

__[Compare in Pairs](http://www.geeksforgeeks.org/maximum-and-minimum-in-an-array/)__.

1. If n is odd then initialize min and max as first element.
1. If n is even then initialize min and max as minimum and maximum of the first two elements respectively.
1. For rest of the elements, pick them in pairs and compare their maximum and minimum with max and min respectively. 

Number of comparison is 1.5*n. 

There's also a __Tournament Method__ from G4G, but the implementation is a bit difficult. 

### Code

__not written by me__

    public static void minmax2(int[] a) {
        if (a == null || a.length < 1)
            return;

        int min, max;

        // if only one element
        if (a.length == 1) {
            max = a[0];
            min = a[0];
            System.out.println("min: " + min + "\nmax: " + max);
            return;
        }

        if (a[0] > a[1]) {
            max = a[0];
            min = a[1];
        } else {
            max = a[1];
            min = a[0];
        }

        for (int i = 2; i <= a.length - 2;) {
            if (a[i] > a[i + 1]) {
                min = Math.min(min, a[i + 1]);
                max = Math.max(max, a[i]);
            } else {
                min = Math.min(min, a[i]);
                max = Math.max(max, a[i + 1]);
            }

            i = i + 2;
        }

        if (a.length % 2 == 1) {
            min = Math.min(min, a[a.length - 1]);
            max = Math.max(max, a[a.length - 1]);
        }

        System.out.println("min: " + min + "\nmax: " + max);
    }
