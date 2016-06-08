---
layout: post
title: "[Google] Number of distinct substrings "
comments: true
category: q-google

---

### Question 

[link](http://www.quora.com/Given-a-string-how-do-I-find-the-number-of-distinct-substrings-of-the-string)

> Given a string, find the number of distinct substrings of the string. Example:

>input = "aaaa", 
>
>output = 4 (the 4 substrings are "a", "aa", "aaa", "aaaa")

>input = "abcd", 
>
>output = 10 ("a", "b", "c", "d", "ab", "bc", "cd", "abc", "bcd", "abcd")

>input = "banana", 
>
>output = 15 ("a", "an", "ana", "anan", "anana", "b", "ba", "ban", "bana", "banan", "banana", "n", "na", "nan", "nana")

This is also a question on [SPOJ](http://www.spoj.com/problems/DISUBSTR/). 

### Solution

This is a very good question, which tests Suffix tree, LCP and string manipulation knowledges. 

__The solution is to build a suffix tree__. This is because: 

> If you look through the __[prefixes of each suffix](http://qr.ae/6o6Nk)__ of a string, you have covered all substrings of that string. 

There are 2 implementations. First one is slightly simpler. 

#### Implementation 1

__Suffix array + LCP__ (longest common prefix). Take "Banana" as input, then the suffixes: 

    0) BANANA
    1) ANANA
    2) NANA
    3) ANA
    4) NA
    5) A

Sort it: 

    5) A
    3) ANA
    1) ANANA
    0) BANANA
    4) NA
    2) NANA

Then we start calculate number of substring (that is prefixes of suffix). After removing duplicated prefix, the count is: 

    5) A - 1
    3) ANA - 2
    1) ANANA - 2
    0) BANANA - 6
    4) NA - 2
    2) NANA - 2

Total number is: 

    1 + 2 + 2 + 6 + 2 + 2 = 15

But wait, realize something? "A" is simply duplicate substring in "ANA", which appers in "ANANA". Keep this in mind, cuz we need to observe this in the 2nd implementation, too.

Finally, the total number is calculated like this: 

    for each suffix
        ans += length(suffix) - LCP(suffix, previous suffix)

For more details, read [here](http://qr.ae/6o6Nk).

#### Implementation 2

Build a suffix tree, like this: 

{% img middle /assets/images/suffix-tree-banana.png %}

Number of substrings is simply the __sum of levels of each leaf__. For the 3 branches of the suffix tree, number of levels are: 6, 5 and 4 respectively. Total = 15. 
