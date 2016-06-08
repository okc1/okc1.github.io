---
layout: post
title: "[Fundamental] Pattern Searching Algorithms "
comments: true
categories:
- Fundamental
- z-string-search

---

[ref](http://www.geeksforgeeks.org/tag/pattern-searching/page/2/)

### Overview

strStr() is a classic question in CS. There are various ways to solve (which we have discussed before), this is a summarization: 

1. naive - O(m * n) 

1. [KMP](http://www.geeksforgeeks.org/searching-for-patterns-set-2-kmp-algorithm/) - O(n) in worst case

1. [Rabin-Karp](http://www.geeksforgeeks.org/searching-for-patterns-set-3-rabin-karp-algorithm/), rolling hash - between O(m * n) and O(m + n)

    Matches the hash value of the pattern with the hash value of pattern. If the hash values match, then only it starts matching individual characters. 

1. [Modified naive algo](http://www.geeksforgeeks.org/pattern-searching-set-4-a-naive-string-matching-algo-question/), only work if pattern contains no duplicate characters. 

    Only match the first char. This case is quite boring, can skip. 

1. Suffix tree

    Will discuss in details. 
