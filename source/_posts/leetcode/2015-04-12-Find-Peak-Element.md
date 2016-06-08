---
layout: post
title: "[LeetCode 162] Find Peak Element "
comments: true
category: Leetcode
---

### Question 

[link](https://leetcode.com/problems/find-peak-element/)

<div class="question-content">
              <p></p><p>A peak element is an element that is greater than its neighbors.</p>

<p>Given an input array where <code>num[i] ? num[i+1]</code>, find a peak element and return its index.</p>

<p>The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.</p>

<p>You may imagine that <code>num[-1] = num[n] = -8</code>.</p>

<p>For example, in array <code>[1, 2, 3, 1]</code>, 3 is a peak element and your function should return the index number 2.</p>

<p class="showspoilers"><a href="#" onclick="showSpoilers(this); return false;">click to show spoilers.</a></p>

<div class="spoilers" style="display: none;"><b>Note:</b>
<p>Your solution should be in logarithmic complexity.</p>
</div>

<p><b>Credits:</b><br>Special thanks to <a href="https://oj.leetcode.com/discuss/user/ts">@ts</a> for adding this problem and creating all test cases.</p><p></p>
              
                <div id="tags" class="btn btn-xs btn-warning">Show Tags</div>
                <span class="hide">
                  
                  <a class="btn btn-xs btn-primary" href="/tag/array/">Array</a>
                  
                  <a class="btn btn-xs btn-primary" href="/tag/binary-search/">Binary Search</a>
                  
                </span>
              
            </div>

### Analysis

This basically is a binary search question. Instead of checking the values, we check the slope (upgoing or downslope). 

__The important point__ is the special cases like [1, 2, 3] or [3, 2, 1], we need to return the corner values. Well there're 2 ways to handle these corner cases. 

### Solution

First, referring to [G4G](http://www.geeksforgeeks.org/find-a-peak-in-a-given-array/), the corner case is handled in this way: 

    if ((mid == 0 || arr[mid-1] <= arr[mid]) &&
            (mid == n-1 || arr[mid+1] <= arr[mid]))
        return mid;

The code 1 below is doing similar things. That code is readable and easy to come up with. I recommend this solution during a interview. 

For those who are interested, there is a extremely concise solution thanks to [Duplan](http://blog.csdn.net/u010367506/article/details/41943309). I have the Java version posted below as code 2. 

### Code

Code 1

    public class Solution {
        public int findPeakElement(int[] num) {
            if (num == null || num.length == 0) {
                return 0;
            } else if (num.length == 1) {
                return 0;
            } else if (num[0] > num[1]) {
                return 0;
            } else if (num[num.length - 2] < num[num.length - 1]) {
                return num.length - 1;
            }
            // now the leftmost edge is increasing
            // and the rightmost edge is also increasing backwards
            return helper(num, 0, num.length - 1);
        }

        public int helper(int[] num, int left, int right) {
            int mid = left + (right - left) / 2;
            if (left + 2 == right) {
                return mid;
            } else if (num[mid] > num[mid + 1]) {
                // middle is decreasing, so peak on the left side
                return helper(num, left, mid + 1);
            } else {
                return helper(num, mid, right);
            }
        }
    }

Code 2

    public class Solution {
        public int findPeakElement(int[] num) {
            if (num == null || num.length == 0) {
                return 0;
            }
            return helper(num, 0, num.length - 1);
        }

        public int helper(int[] num, int left, int right) {
            int mid = left + (right - left) / 2;
            if (left == right) {
                return left;
            } else if (num[mid] > num[mid + 1]) {
                // middle is decreasing, so peak on the left side
                return helper(num, left, mid);
            } else {
                return helper(num, mid + 1, right);
            }
        }
    }
