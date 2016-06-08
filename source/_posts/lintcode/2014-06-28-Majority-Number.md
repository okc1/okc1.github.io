---
layout: post
title: "[LintCode] Majority Number "
comments: true
category: LintCode

---


### Question 

[link](http://www.lintcode.com/en/problem/majority-number/)

> How to find the majority elelment in an array in O(n)?

> Note: The majority element is the element that occurs more than half of the size of the array

> Example: For [1, 1, 1, 1, 2, 2, 2], return 1

### Analysis 

This question is called __[Moore’s Voting Algorithm](http://www.cs.utexas.edu/~moore/best-ideas/mjrty/example.html)__ (or Majority Vote Algorithm). 

Psudo-code from [GFG](http://www.geeksforgeeks.org/majority-element/): 

    findCandidate(a[], size)
    1.  Initialize index and count of majority element
         maj_index = 0, count = 1
    2.  Loop for i = 1 to size – 1
        (a)If a[maj_index] == a[i]
            count++
        (b)Else
            count--;
        (c)If count == 0
            maj_index = i;
            count = 1
    3.  Return a[maj_index]

Sometimess majority element does not exist, so you might want to do another iteration to double check. 

If the check shows invalid, then there's no majoirty element. 

### Code

    public int majorityNumber(ArrayList<Integer> nums) {
        // write your code
        if (nums == null || nums.size() == 0) {
            return 0;
        }
        int num = nums.get(0);
        int count = 1;
        for (int i = 1; i < nums.size(); i++) {
            if (count == 0) {
                num = nums.get(i);
                count = 1;
            } else if (nums.get(i) == num) {
                count++;
            } else {
                count--;
            }
        }
        return num;
    }
