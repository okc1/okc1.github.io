---
layout: post
title: "[Google] Check all numbers given the decimal scale "
comments: true
category: q-google

---

### Question 

[link](http://www.mitbbs.com/article_t/JobHunting/32859887.html)

> 检查一个字符串是否包含k位a进制数的所有表示形式。

> 保证原字符串的所有字串都是合法的k位a进制数。

> "00110, a=2, k=2" => true （包括了00，01，10，11）

### Solution

First find all substrings with length == k, then generate all numbers in a scale. This is not a difficult question. 

We may want to score the substrings in a HashMap/HashSet. __The hashing procedure is preferrably using [Rolling hash](http://en.wikipedia.org/wiki/Rolling_hash)__. 

> Rolling Hash

> A rolling hash is a hash function where the input is hashed in a window that moves through the input.

> A few hash functions allow a rolling hash to be computed very quickly—the new hash value is rapidly calculated given only the old hash value, the old value removed from the window, and the new value added to the window—similar to the way a moving average function can be computed much more quickly than other low-pass filters.

Rolling Hash is commonly used in __[Rabin-Karp Algorithm](http://www.geeksforgeeks.org/searching-for-patterns-set-3-rabin-karp-algorithm/)__ to speed up strStr() string pattern matching. 

People in the origin post - they discuss about "__slide window check__" algorithm. I do not understand what's the benefit of this. If you read this and would like to help me, please leave a comment. Thanks! 

### A similar question

[This](http://www.mitbbs.com/article_t/JobHunting/32860321.html) is simply the reverse of the question above: 

> 给出最短的字符串, which is used to 表示k位a进制数的所有表示形式. 

This question is solved using __[De Bruijn sequence](http://en.wikipedia.org/wiki/De_Bruijn_sequence)__. 
