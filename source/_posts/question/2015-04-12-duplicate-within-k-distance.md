---
layout: post
title: "[Palantir] Find Duplicate within K Distance "
comments: true
category: Question

---

### Question 

[link](http://www.careercup.com/question?id=18517665)

> Given an array of values, design and code an algorithm that returns whether there are two duplicates within k indices of each other? 

### Solution

We can keep a HashMap for storing the previous occuring position of a number. 

### Code

    public boolean dupWithinK(int k, int[] arr) {
        Set<Integer> set = new HashSet<Integer>();
        for (int i = 0; i < arr.length; i++) {
            if (set.contains(arr[i])) {
                return true;
            }
            if (i < k) {
                // the first k numbers
                set.add(arr[i]);
            } else {
                // the (k+1) th number and onwards
                set.add(arr[i]);
                set.remove(arr[i - k]);
            }
        }
        return false;
    }
