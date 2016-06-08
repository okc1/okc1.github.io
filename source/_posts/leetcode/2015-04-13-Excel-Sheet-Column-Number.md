---
layout: post
title: "[LeetCode 171] Excel Sheet Column Number "
comments: true
category: Leetcode
---

### Question 

[link](https://leetcode.com/problems/excel-sheet-column-number/)

<div class="question-content">
              <p></p><p>Related to question <a href="https://oj.leetcode.com/problems/excel-sheet-column-title/">Excel Sheet Column Title</a></p>
<p>Given a column title as appear in an Excel sheet, return its corresponding column number.</p>

<p>For example:</p>
<pre>    A -&gt; 1
    B -&gt; 2
    C -&gt; 3
    ...
    Z -&gt; 26
    AA -&gt; 27
    AB -&gt; 28 </pre>

<p><b>Credits:</b><br>Special thanks to <a href="https://oj.leetcode.com/discuss/user/ts">@ts</a> for adding this problem and creating all test cases.</p><p></p>
              
                <div id="tags" class="btn btn-xs btn-warning">Show Tags</div>
                <span class="hide">
                  
                  <a class="btn btn-xs btn-primary" href="/tag/math/">Math</a>
                  
                </span>
              
            </div>

### Analysis

This question I've seen it quite a few time. It's very standard integer conversion question. 

### Solution

Please read this post __[[ItInt5] Excel Decimal Conversion]({% post_url /question/2014-08-16-Excel-decimal-conversion %})__. 

### Code

recursively:

    public class Solution {
        public String convertToTitle(int n) {
            if (n < 1) {
                return "";
            }
            n--;
            char ch = (char) ((n % 26) + 'A');
            return convertToTitle(n / 26) + ch;
        }
    }
