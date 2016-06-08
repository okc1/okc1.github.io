---
layout: post
title: "[NineChap 1.1] strStr and Coding Style"
comments: true
category: NineChap

---


## strStr Question

__[Implement strStr]({% post_url /leetcode/2014-05-10-Implement-strStr %})__

Before solving the problem, it's very important to ask this questions: 

> __Can we use system library (eg. str.substring() or indexOf())__

The answer is 'No', but asking this question shows that you think deep into questions. Keep in mind the characteristics for a candidate is judged by 4 things: 

1. Code readability - how long does it take to review your code?
1. Coding convention - do you have the habit to write efficient code?
1. Testing - it's good habit to write test case before asked to. 
1. Communication skills

Solution of this question is double for-loop. It's not linear time complexity, but it's OK. After getting the code correct, it's best to tell the O(n) time KMP solution. However, it's most probably not required to implement. 

__my code__

    public String strStr(String haystack, String needle) {
        if (haystack == null || needle == null) {
            return null;
        }
        int len1 = haystack.length();
        int len2 = needle.length();
        for (int i = 0; i <= len1 - len2; i ++) {
            // start from i, match chars
            boolean match = true;
            for (int j = 0; j < len2; j ++) {
                if (haystack.charAt(i + j) != needle.charAt(j)) {
                    match = false;
                    break;
                }
            }
            if (match) {
                return haystack.substring(i);
            }
        }
        return null;
    }

alternative code from [ninechap](http://answer.ninechapter.com/solutions/implement-strstr/)

    public String strStr(String haystack, String needle) {
        if(haystack == null || needle == null) {
            return null;
        }
        int i, j;
        for(i = 0; i < haystack.length() - needle.length() + 1; i++) {
            for(j = 0; j < needle.length(); j++) {
                if(haystack.charAt(i + j) != needle.charAt(j)) {
                    break;
                }
            }
            if(j == needle.length()) {
                return haystack.substring(i);
            }
        }
        return null;
    }

## Google Coding Style

#### if ... else ...

    if (condition) {
        statements;
    } else if (condition) {
        statements;
    } else {
        statements;
    }

#### 自增/自减

    while （d++ = s++） {
        n++;
    }

To be continued. 
