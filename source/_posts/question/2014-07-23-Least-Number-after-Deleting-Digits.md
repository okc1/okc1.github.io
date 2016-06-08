---
layout: post
title: "[Question] Least Number after Deleting Digits"
comments: true
category: Question
tags: [ unit test needed ]
---

### Question 

[link](http://codercareer.blogspot.sg/2013/11/no-48-least-number-after-deleting-digits.html)

> Please get the least number after deleting k digits from the input number. 

> For example, if the input number is 24635, the least number is 23 after deleting 3 digits. 

### Analysis

There's a solution which instead of 'delete k', find the smallest number by 'keeping (n-k) numbers'. It's more strightforward. 

### Solution

1. From the start, search till the end.
    1. If a digit is greater than next one, delete it. 
    1. If all digits are increasingly sorted, delete last. 
1. Each time go back to start to search again. 

Example

> 24635 -> 2435 -> 235 -> 23

### Code

from Harry He

    public static String getLeastNumberDeletingDigits_1(String number, int k) {
        String leastNumber = number;
        while(k > 0 && leastNumber.length() > 0) {
            int firstDecreasingDigit = getFirstDecreasing(leastNumber);
            if(firstDecreasingDigit >= 0) {
                leastNumber = removeDigit(leastNumber, firstDecreasingDigit);
            }
            else {
                leastNumber = removeDigit(leastNumber, leastNumber.length() - 1);
            }

            --k;
        }

        return leastNumber;
    }

    private static int getFirstDecreasing(String number) {
        for(int i = 0; i < number.length() - 1; ++i) {
            int curDigit = number.charAt(i) - '0';
            int nextDigit = number.charAt(i + 1) - '0';
            if(curDigit > nextDigit) {
                return i;
            }
        }

        return -1;
    }

    private static String removeDigit(String number, int digitIndex) {
        String result = "";
        if(digitIndex > 0) {
            result = number.substring(0, digitIndex);
        }
        if(digitIndex < number.length() - 1) {
            result += number.substring(digitIndex + 1);
        }

        return result;
    }
