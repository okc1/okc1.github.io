---
layout: post
title: "[Amazon] Match triplet with reverse order "
comments: true
categories:
- Question
- z-string-search

---

### Question

[link](http://www.careercup.com/question?id=11655778)

> Find the substring of length 3 which is present in the reverse order from the string. 

> Ex: if the string is abcdcba (cba is the reverse of abc) so we should return cba. 

### Solution

1. __HashMap (recommended)__. Hash all substrings of length 3. O(n). Look up all reverse substrings of length 3 in this hash set. O(n) time and O(n) space. 

1. __KMP Algo__. Take every substring of length 3. Reverse it and find it in the input using KMP. O(n^2) time and O(1) space. 

1. __Build suffix tree__ of height 3. Then in reverse order, check triplets. 

The 3 solutions above all work well. Pick the one you love. 
