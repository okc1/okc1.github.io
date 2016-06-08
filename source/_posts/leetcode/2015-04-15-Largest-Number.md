---
layout: post
title: "[LeetCode 179] Largest Number "
comments: true
category: Leetcode
---

### Question

[link](https://leetcode.com/problems/largest-number/)

<div class="question-content">
              <p></p><p>Given a list of non negative integers, arrange them such that they form the largest number.</p>

<p>For example, given <code>[3, 30, 34, 5, 9]</code>, the largest formed number is <code>9534330</code>.</p>

<p>Note: The result may be very large, so you need to return a string instead of an integer.</p>

<p><b>Credits:</b><br>Special thanks to <a href="https://oj.leetcode.com/discuss/user/ts">@ts</a> for adding this problem and creating all test cases.</p><p></p>

                <div id="tags" class="btn btn-xs btn-warning">Show Tags</div>
                <span class="hide">

                  <a class="btn btn-xs btn-primary" href="/tag/sort/">Sort</a>

                </span>

            </div>

### Analysis

Please refer to [[ItInt5] Numbers Concatenation Max (Largest Number)({% post_url /question/2014-08-17-Numbers-Concatenation-Max %}).

### Solution

Note that we __can not override Comparator(Integer)__. So we must first convert int to string then sort.

### Code

    public class Solution {

        // this code should pass
        public String largestNumber(int[] num) {
            if (num == null || num.length == 0) {
                return "0";
            }
            String[] strs = new String[num.length];
            for (int i = 0; i < num.length; i++) {
                strs[i] = String.valueOf(num[i]);
            }
            Arrays.sort(strs, new LargerComparator());

            String res = "";
            for (String str : strs) {
                res = res + str;
            }
            return res;
        }

        class LargerComparator implements Comparator<String> {

            public int compare(String a, String b) {
                String first = a + b;
                String second = b + a;
                return second.compareTo(first);
            }
        }
    }
