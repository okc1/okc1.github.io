---
layout: post
title: "[Brain teaser] 6.1 Bottles of Pills "
comments: true
category: CC150v5

---

### Question

> You have 20 bottles of pills. 19 bottles have 1.0 gram pills, but one has pills of weight 1.1 grams. 

> Given a scale, how to find the heavy bottle __only scaling ONCE__? 

### Solution

Take 1 pill from Bottle 1, 2 pills from Bottle 2, and so on. We'll expect (1 + 2 + ... + 20) = 210 gram of pills. 

The answer would be {(weight - 210 grams) / 0.1}. 
