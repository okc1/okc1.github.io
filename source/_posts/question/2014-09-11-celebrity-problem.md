---
layout: post
title: "[Question] Celebrity Problem "
comments: true
category: Question

---

### Question

[link](http://www.careercup.com/question?id=13167666)

> You have a room with n people. A celebrity walks in. Everyone knows the celebrity, the celebrity knows no one. 

> Non-celebrities may/may not know anyone in the room. 

> Give an algorithm to find the celebrity. Discuss the complexity. 

### Solution

[Classic brute-force solution](http://www.geeksforgeeks.org/the-celebrity-problem/) would take O(n^2) time to build a map. That's not good, and we have a very simple solution that works in O(n) time: 

> Make all of them stand in a row. Let's say the people are a,b,c,d,e,f,g,h,i,j,.......n 

> Compare a and b. __If a knows b__, a is not celebrity. __If a doesn't know b__, b is not celebrity. 

> At the end, the probable celebrity who survives is the certain celebrity. (better do a check)

Total number of comparison is [3(N-1) times](http://www.geeksforgeeks.org/the-celebrity-problem/). 

### Code

__not written__

