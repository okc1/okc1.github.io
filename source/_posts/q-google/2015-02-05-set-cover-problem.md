---
layout: post
title: "[Google] Set Cover Problem "
comments: true
category: q-google

---

### Question 

[link](http://www.mitbbs.com/article_t/JobHunting/32547841.html)

> Give a list of documents, find the minimal document set that can 
cover all the characters in all the documents. 

> eg. 

    “a b c h j”,  
    "c d”, 
    “a b c” 
    “a f g” 
    “a h j”

> The result should be 

    "a b c h j" 
    "c d" and 
    "a f g"

### Solution 

[Set cover problem](http://en.wikipedia.org/wiki/Set_cover_problem) is NP. 

__DP solution is available__ [here](http://www.mimuw.edu.pl/~malcin/dydaktyka/2012-13/fpt/fpt_04_FSC-kociumaka.pdf), with O(2 ^ n) time complexity. 

> T[i][X] denotes the minimal number of sets out of {S1, S2, . . . , Si} that covers X.

> So we have: 

> T[i][X] = min(1 + T[i − 1][X - Si], T[i − 1][X])

### Code

not written
