---
layout: post
title: "[Question] Bucket Sort (bin sort)"
comments: true
category: Question

---

### Question 

[link](http://www.geeksforgeeks.org/bucket-sort-2/)

> Bucket sort is mainly useful when input is uniformly distributed over a range. For example: 

> Sort a large set of floating point numbers which are in range from 0.0 to 1.0 and are uniformly distributed across the range. How do we sort the numbers efficiently.

### Solution

1) Create n empty buckets (Or lists).

2) Insert each arr[i] into bucket[n*array[i]]

3) Sort individual buckets using __insertion sort__.

4) Concatenate all sorted buckets.

Steps 1 and 2 clearly take O(n) time. Step 4 also takes O(n) time. 

__The main step to analyze is step 3__. This step also takes O(n) time on average if all numbers are uniformly distributed. __Final time complexity: O(n)__. 

### Relationship with other sorting algorithms

There's a algorithm within the bucket. Now if we use __bucket sort itself__ as the sorting function, this becomes a __radix sort__. 

If we set the __bucket size as 2__, then this becomes a quick sort (with potentially poor pivot choices). 

### Code

C++ code from G4G

    void bucketSort(float arr[], int n) {
        // 1) Create n empty buckets
        vector<float> b[n];

        // 2) Put array elements in different buckets
        for (int i=0; i<n; i++)
        {
           int bi = n*arr[i]; // Index in bucket
           b[bi].push_back(arr[i]);
        }

        // 3) Sort individual buckets
        for (int i=0; i<n; i++)
           sort(b[i].begin(), b[i].end());

        // 4) Concatenate all buckets into arr[]
        int index = 0;
        for (int i = 0; i < n; i++)
            for (int j = 0; j < b[i].size(); j++)
              arr[index++] = b[i][j];
    }
