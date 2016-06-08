---
layout: post
title: "[Greedy] Each Employee 2 events "
comments: true
category: Question

---

[link](http://www.careercup.com/question?id=7894677)

### Question 

> You are given N ranges of date offsets when N employees are present in an organization. Something like 

        1-4 (i.e. employee will come on 1st, 2nd, 3rd and 4th day ) 
        2-6 
        8-9 
        .. 
        1-14 

> Organize an event on minimum number of days such that each employee can attend the event at least twice.

### Solution

__Greedy algorithm__, according to the [top answer](http://www.careercup.com/question?id=7894677): 

1. First, sort all ranges based on ENDING date in increasing order (bucket or counting sort). 

1. For each range, select last two days (because they produce maximum possibility to overlap next range) 

1. Skip following ranges that also contains those two days, until:

    1. a range that either covers only one day (we then select last day of this range) or 
    1. does not cover any of the two (we then select last two days of this range). 

1. Then continue.

### Code

not written
