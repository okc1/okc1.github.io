---
layout: post
title: "[Question] Check string with no common letters (Bitmask) "
comments: true
category: Question

---

### Question 

RT. This is a very very common requirements in the area of string manipulation. We want it to be done very efficiently. 

### Solution

Normally, we would use a hashmap. However, we can also use __bitmask__ or bitmap. 

Work for a-z only, we use 1 integer to represent each letter, and set an integer for each string. 

We do (mask1 & mask2 == 0) to find no common letters. Read more at this question, __[Google] Max prodcut of strings that have no common char__. 
