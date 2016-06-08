---
layout: post
title: "[LeetCode 164] Maximum Gap "
comments: true
category: Leetcode
---

### Question 

[link](https://leetcode.com/problems/maximum-gap/)

<div class="question-content">
              <p></p><p>Given an unsorted array, find the maximum difference between the successive elements in its sorted form.</p>

<p>Try to solve it in linear time/space.</p>

<p>Return 0 if the array contains less than 2 elements.</p>

<p>You may assume all elements in the array are non-negative integers and fit in the 32-bit signed integer range.</p>

<p><b>Credits:</b><br>Special thanks to <a href="https://oj.leetcode.com/discuss/user/porker2008">@porker2008</a> for adding this problem and creating all test cases.</p><p></p>
              
                <div id="tags" class="btn btn-xs btn-warning">Show Tags</div>
                <span class="hide">
                  
                  <a class="btn btn-xs btn-primary" href="/tag/sort/">Sort</a>
                  
                </span>
              
            </div>

### Analysis

__This is an extremely difficult question__ of bucket sort. I refered to [programcreek](http://www.programcreek.com/2014/03/leetcode-maximum-gap-java/) and [tgic's blog](http://leetcode.tgic.me/maximum-gap/index.html) for reference. 

### Solution

__Basic idea is to put elements into buckets__. The number of bucket is (almost) same as the number of elements in the input. In this way, each bucket __ideally__ will contain 1 element. 

We then know that __the max gap must be cross-bucket instead of within bucket__. So we simply keep track of max and min value within each bucket for the purpose of calculating gap. 

__Why did I say "number of bucket is (almost) same as the number of elements in the input"__? Well, consider this case: 3 values and (maxVal - minVal) == 100. We can make 3 bucket with size = 34. How about 5 values and (maxVal - minVal) == 6? Bucket size shall be either 1 or 2. So we'll have either 3 or 6 bucket. 

So, in the code below, you can see I make bucket size "larger by 1": 

    // bSize is size of bucket (should be larger by 1)
    int bSize = (maxVal - minVal + 1) / num.length + 1;

    // calcualte number of buckets needed
    int bCount = (maxVal - minVal) / bSize + 1;
    Bucket[] buckets = new Bucket[bCount];


Note that simply use __input.length__ as bucket count is wrong. 

### Code

My code written in Java:

    public class Solution {
        public int maximumGap(int[] num) {
            if (num == null || num.length < 2) {
                return 0;
            }

            // find out max and min values of input
            int minVal = num[0];
            int maxVal = num[0];
            for (int n: num) {
                minVal = Math.min(minVal, n);
                maxVal = Math.max(maxVal, n);
            }
            // bSize is size of bucket (should be larger by 1)
            int bSize = (maxVal - minVal + 1) / num.length + 1;

            // calcualte number of buckets needed
            int bCount = (maxVal - minVal) / bSize + 1;
            Bucket[] buckets = new Bucket[bCount];

            // match every value into a bucket
            // bucket maintains the max/min within the bucket
            for (int n: num) {
                int bIndex = (n - minVal) / bSize;
                if (buckets[bIndex] == null) {
                    buckets[bIndex] = new Bucket(n, n);
                } else {
                    buckets[bIndex].updateVal(n);
                }
            }

            // for every bucket, check in sequence and get max gap
            int gap = 0;
            int pre = 0;
            int cur = 1;
            while (cur < bCount) {
                // skip all empty buckets
                while (cur < bCount && buckets[cur] == null) {
                    cur++;
                }
                if (cur == bCount) break;
                // update gap, pre and cur
                gap = Math.max(gap, buckets[cur].min - buckets[pre].max);
                pre = cur;
                cur++;
            }

            return gap;
        }

        class Bucket {
            int min;
            int max;

            public Bucket(int a, int b) {
                min = a;
                max = b;
            }

            public void updateVal(int val) {
                min = Math.min(min, val);
                max = Math.max(max, val);
            }
        }
    }
