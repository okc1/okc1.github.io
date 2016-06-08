---
layout: post
title: "[LintCode] Majority Number II"
description: ""
category: LintCode

---

### Question 

[link](http://www.lintcode.com/en/problem/majority-number-ii/)

> Given an array of integers, the majority number is the number that occurs more than 1/3 of the size of the array. Find it.

> Note: There is only one majority number in the array

> Example: For [1, 2, 1, 2, 1, 3, 3] return 1

### Analysis 

Similar to 'Majority Number', but a little more difficult. 

__Instead of keeping 1 value for checking, now keep 2 values__. If the new number is same as any of the 2 values, decrease the count. If the new number is a totally new one, decrease both. The coding is a bit difficult and lengthy. 

Note that 2 values are found in the end, do another iteration thru the array, and find the correct result from these 2 values. 

### Code

    public int majorityNumber(ArrayList<Integer> nums) {
        // write your code
        if (nums == null || nums.size() < 3) {
            return -1;
        }
        int num1 = nums.get(0);
        int p = 1;
        int len = nums.size();
        while (p < len && nums.get(p) == num1) {
            p++;
        }
        int num2 = nums.get(p);
        int count1 = p;
        int count2 = 1;
        for (int i = p + 1; i < len; i++) {
            if (nums.get(i) == num1) {
                count1++;
            } else if (nums.get(i) == num2) {
                count2++;
            } else {
                // a totally different value
                if (count1 == 0) {
                    num1 = nums.get(i);
                    count1++;
                } else if (count2 == 0) {
                    num2 = nums.get(i);
                    count2++;
                } else {
                    count1--;
                    count2--;
                }
            }
        }
        if (count1 == 0 && count2 == 0) {
            return -1;
        } else if (count1 == 0) {
            return num2;
        } else if (count2 == 0) {
            return num1;
        } else {
            // it's gotta be either num1 or num2
            int count = 0;
            for (Integer n: nums) {
                if (n == num1) {
                    count ++;
                }
            }
            if (count >= len / 3 + 1) {
                return num1;
            } else {
                return num2;
            }
        }
    }
