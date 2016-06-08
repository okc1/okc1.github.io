---
layout: post
title: "[Google] Traveller Path Problem "
comments: true
category: q-google

---

### Question 

[link](http://www.careercup.com/question?id=5749537700315136)

> Traveler wants to travel from city “A” to city “D”. There is a path from city “A” to city “D”. Path consists of steps, i.e. travel from city “A” to city “B”. Path is encoded as sequence of steps. 

> Sequence is in incorrect order. Your task is to restore order of steps in the path. 

> Input (unordered sequence): 

    C -> D 
    A -> B 
    B -> C 

> Output (Correctly ordered list which represents path): 

    A, B, C, D 

> Implement following API:

    class Step {
        String start;
        String finish;
    };

    class Node {
        String value;
        Node next;
    }

    List<String> findPath(List<Step> steps) {
    }

### Solution

This question is not stated clear enough. I found one tentative algorithm: 

> First, initialize a result - sortedPath, and build 2 maps (String to String) - startsToFinishes and finishesToStarts (O(N)) 

> Then, find the one key on startsToFinishes, that is not a key in finishesToStarts - this is the city from which the path begins. (O(N)) 

> Then, iteratively, city by city, build the path. 

__Follow up on Sep 2nd, 2014__: 

[This post](http://www.mitbbs.com/article_t/JobHunting/32772275.html) talks about this question. The answer would be similar to what's writtne above. 
