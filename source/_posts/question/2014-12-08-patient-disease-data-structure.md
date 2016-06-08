---
layout: post
title: "[Epic] Patient Disease Data Structure "
comments: true
category: Question

---

### Question 

[link](http://www.mitbbs.com/article_t0/JobHunting/32844253.html)

> Suppose N patients and M diseases. N is sufficiently large number and M is 
relatively small, say 30-ish. Each patient can have possible 0 to M kinds of
diseases.

> Given one patient’s name, show me a list of similar patients sharing same 
deseases within 2-3 seconds.

### Solution

__Use 1 bit to represent a disease__. So every patient's conditin can be put into an integer of 32 bits. 

How do we calculate the similarity of 2 patients?

Refer to __[CC150v5] 5.5 Calculate Bits Conversion Required__ for a special bit operation (remove last '1' from bit): 

> c = c & (c - l) clears the least significant bit of '1'. 
>
> Keep doing this until all '1's are cleared. 

For each patient, we simply calculate the XOR and count '1's. 

### Code

no code. 
