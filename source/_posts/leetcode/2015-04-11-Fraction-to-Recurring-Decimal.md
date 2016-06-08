---
layout: post
title: "[LeetCode 166] Fraction to Recurring Decimal "
comments: true
category: Leetcode
---

### Question 

[link](https://leetcode.com/problems/fraction-to-recurring-decimal/)

<div class="question-content">
              <p></p><p>Given two integers representing the numerator and denominator of a fraction, return the fraction in string format.</p>

<p>If the fractional part is repeating, enclose the repeating part in parentheses.</p>
<p>
For example,
</p><ul>
<li>Given numerator = 1, denominator = 2, return "0.5".</li>
<li>Given numerator = 2, denominator = 1, return "2".</li>
<li>Given numerator = 2, denominator = 3, return "0.(6)".</li>
</ul>
<p></p>

<p><b>Credits:</b><br>Special thanks to <a href="https://oj.leetcode.com/discuss/user/Shangrila">@Shangrila</a> for adding this problem and creating all test cases.</p><p></p>
              
                <div id="tags" class="btn btn-xs btn-warning">Show Tags</div>
                <span class="hide">
                  
                  <a class="btn btn-xs btn-primary" href="/tag/hash-table/">Hash Table</a>
                  
                  <a class="btn btn-xs btn-primary" href="/tag/math/">Math</a>
                  
                </span>
</div>

### Analysis

Wow, this is just another incredible question on Leetcode. Quite a few difficult corner cases in the OJ. 

Current AC rate is first lowest at 12.4%. 

### Solution

There're 3 things that we must take note: 

1. Handle positive/nagetive cases well. Note that both numerator and denominator can be negative number. And there're also case like: 

> 1 / -3 = -0.(3)

2. Note that we have to match the repetation of the actual numerator. Not the quotient. What do I mean by that? 

>1 / 6 = 0.1(6)
>
>1 / 333 = 0.(003)
    
3. Note below is __how to override the equals() method__ (first one is wrong and second is right): 

    public boolean equals(Pair p) {
        
    }

    public boolean equals(Object obj) {
        
    }

__One more thing__: Most other guys' solutions like [this](http://www.programcreek.com/2014/03/leetcode-fraction-to-recurring-decimal-java/), [this](http://blog.csdn.net/ljiabin/article/details/42025037) and [this](http://yuanhsh.iteye.com/blog/2176178) are using Hashing. It's fine and definitely good. I used linearly search though, which is a small time compromise. I am presenting my code below and please just consider it as something different. Keep in mind it's not the optimized solution. 

### Code

    public class Solution {
        public String fractionToDecimal(int numerator, int denominator) {
            long quotient = (long) numerator / denominator;
            long reminder = (long) numerator % denominator;
            if (reminder == 0) {
                return String.valueOf(quotient);
            }

            // The result has 3 parts: sign, integer part, and fraction part
            // eg. -4 / 3 = -1 and the result of (1/3) = (3)
            String sign = ((long) numerator * denominator >= 0) ? "" : "-";
            long integer = Math.abs(quotient);
            String fraction = fraction(Math.abs((long)reminder), Math.abs((long)denominator));

            // why do we have to seperate sign from integer?
            // cuz 1 / -3 = -0.(3), while quotient is 0. 
            // So, we can't simply concatenate quotient with fraction
            return sign + integer + "." + fraction;
        }

        String fraction(long num, long denum) {
            // eg. num = 1, denum = 4, should return "25"

            List<Pair> list = new ArrayList<Pair>();
            String result = "";
            while (num != 0) {
                num *= 10;
                long digit = num / denum;

                // eg. 1 / 333 = (003), so the pairs would be like this:
                // {10, 0}, {100, 0}, {1000, 3}, {10, 0}...
                Pair cur = new Pair(num, digit);
                num %= denum;

                // now add cur Pair to the list
                if (list.indexOf(cur) == -1) {
                    list.add(cur);
                } else {
                    // found a recurring dicimal in the previous output stream
                    int pos = list.indexOf(cur);
                    for (int i = 0; i < pos; i++) {
                        result += list.get(i).digit;
                    }
                    result += "(";
                    for (int i = pos; i < list.size(); i++) {
                        result += list.get(i).digit;
                    }
                    result += ")";
                    break;
                }
            }

            // if there is recurring digit, the result should have already been generated
            if (result.length() == 0) {
                for (Pair p: list) {
                    result += p.digit;
                }
            }
            return result;
        }

        class Pair {
            long num;
            long digit;

            public Pair(long a, long b) {
                num = a;
                digit = b;
            }

            public boolean equals(Object obj) {
                // note the equals interface passes in (Object obj)
                // instead of a Pair object
                Pair p = (Pair) obj;
                return this.num == p.num && this.digit == p.digit;
            }
        }
    }

