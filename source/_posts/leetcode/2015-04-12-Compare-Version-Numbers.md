---
layout: post
title: "[LeetCode 165] Compare Version Numbers "
comments: true
category: Leetcode
---

### Question 

[link](https://leetcode.com/problems/compare-version-numbers/)

<div class="question-content">
              <p></p><p>Compare two version numbers <i>version1</i> and <i>version2</i>.<br>
If <i>version1</i> &gt; <i>version2</i> return 1, if <i>version1</i> &lt; <i>version2</i> return -1, otherwise return 0.</p>

<p>You may assume that the version strings are non-empty and contain only digits and the <code>.</code> character.<br>
The <code>.</code> character does not represent a decimal point and is used to separate number sequences.<br>
For instance, <code>2.5</code> is not "two and a half" or "half way to version three", it is the fifth second-level revision of the second first-level revision.</p>

<p>Here is an example of version numbers ordering:</p>
<pre>0.1 &lt; 1.1 &lt; 1.2 &lt; 13.37</pre>

<p><b>Credits:</b><br>Special thanks to <a href="https://oj.leetcode.com/discuss/user/ts">@ts</a> for adding this problem and creating all test cases.</p><p></p>
              
                <div id="tags" class="btn btn-xs btn-warning">Show Tags</div>
                <span class="hide">
                  
                  <a class="btn btn-xs btn-primary" href="/tag/string/">String</a>
                  
                </span>
              
            </div>

### Analysis

I've seen a couple of interesting ideas on other people's blogs, including [one](http://www.programcreek.com/2014/03/leetcode-compare-version-numbers-java/) that uses String.split() to convert input to an array, and [this one](http://www.meetqun.com/thread-3331-1-1.html) which uses 2 pointers to compare. 

My solution might seem more intuitive for some. See below for my solution. 

### Solution

The idea is to identify what the current number is (before end of string, or before the next '.'). If there's no more string, value = 0, so the case of (1.0, 1) essentially equals. Without further ado, let's look at the code. 

### Code

    public class Solution {
        public int compareVersion(String version1, String version2) {
            if (version1 == null || version2 == null) {
                return 0;
            }
            return helper(version1, version2);
        }

        private int helper(String v1, String v2) {
            if (v1.length() == 0 && v2.length() == 0) {
                return 0;
            }

            int num1 = 0;
            int num2 = 0;

            if (v1.length() != 0) {
                int p1 = 0;
                while (p1 < v1.length() && v1.charAt(p1) != '.') {
                    p1++;
                }
                num1 = Integer.parseInt(v1.substring(0, p1));
                if (p1 < v1.length()) p1++;
                v1 = v1.substring(p1);
            }

            if (v2.length() != 0) {
                int p2 = 0;
                while (p2 < v2.length() && v2.charAt(p2) != '.') {
                    p2++;
                }
                num2 = Integer.parseInt(v2.substring(0, p2));
                if (p2 < v2.length()) p2++;
                v2 = v2.substring(p2);
            }

            if (num1 != num2) {
                return (num1 - num2) / Math.abs(num1 - num2);
            } else {
                return helper(v1, v2);
            }
        }
    }
