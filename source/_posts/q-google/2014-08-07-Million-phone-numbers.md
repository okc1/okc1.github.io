---
layout: post
title: "[Google] Million Phone Numbers"
comments: true
category: q-google

---

### Question 1

[link](http://www.glassdoor.com/Interview/How-would-you-store-1-million-phone-numbers-QTN_456.htm)

> How would you store 1 million phone numbers? 

### Solution

BitMap.

> The key here is that 1 million phone numbers will be within some range, likely 10 million or so. 10 million bits = 10^7 bits ~ 0.12 GB. Just have a bit array where the first bit being set implies that the first phone number is set (e.g., 10 000 000) and the last bit indicates the last phone number (10 999 999). If you find a number in the list, just set the appropriate bit. You now have a bit vector of size 1million bits, sorted, and to check for a particular number, you just check whether the corresponding bit is set.

### Question 2

[link](http://www.careercup.com/question?id=7997766)

> How would you sort 1 million phone numbers? 

### Solution

BitMap or radix sort, both are O(n) complexity.

Read more [here](http://www.vex.net/~trebla/compsci/sorting-phone-numbers.html). 
