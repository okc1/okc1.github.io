---
layout: post
title: "[LeetCode 168] Excel Sheet Column Title "
comments: true
category: Leetcode
---

### Question 

[link](https://leetcode.com/problems/excel-sheet-column-title/)

<div class="question-content">
              <pExcel Sheet Column Number></p><p>Given a positive integer, return its corresponding column title as appear in an Excel sheet.</p>

<p>For example:</p>
<pre>    1 -&gt; A
    2 -&gt; B
    3 -&gt; C
    ...
    26 -&gt; Z
    27 -&gt; AA
    28 -&gt; AB </pre>

<p><b>Credits:</b><br>Special thanks to <a href="https://oj.leetcode.com/discuss/user/ifanchu">@ifanchu</a> for adding this problem and creating all test cases.</p><p></p>
              
                <div id="tags" class="btn btn-xs btn-warning">Show Tags</div>
                <span class="hide">
                  
                  <a class="btn btn-xs btn-primary" href="/tag/math/">Math</a>
                  
                </span>
              
            </div>

### Analysis

This is pretty much a similar question. It's pretty easy. 

### Code

    public class Solution {
        public int titleToNumber(String s) {
            if (s == null || s.length() == 0) {
                return 0;
            }
            int sum = 0;
            for (char ch: s.toCharArray()) {
                sum *= 26;
                sum += (int) (ch - 'A' + 1);
            }
            return sum;
        }
    }

