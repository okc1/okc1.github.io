---
layout: post
title: "[Question] Elephant And Bananas"
comments: true
category: Question
tags: [  ]
---

### Question 

[link](http://tech-queries.blogspot.sg/2011/04/elephant-and-banana.html)

> There's a elephant, which can carry max 1000 bananas. The elephant eats a banana every 1 Km (both forward and back).

> Now we want to transfer 3000 bananas to a place 1000 Km away. How many bananas can be left? 

> Also solved to generalized problem (write code for solution).

### Analysis

__If we subdivide distances for each kilometer__. Notice if elephant wants to shift all the bananas 1 km, __you will loose 5 bananas every km__. 

So we transferred 2995 (998+998+999) to one km distance. This process continues until after 200 km, we have only 2000 bananas left with remaining distance of 800 km. 

__Start from here, we only loose 3 bananas every km__. This goes on for another 334 km, we will have 998 bananas left, and the rest of the bananas can be transfered in a single journey. 

### Solution

__532 bananas__. 
