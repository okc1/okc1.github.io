---
layout: post
title: "[Question] Random Number Generate Question"
comments: true
category: Question

---

### Question 

[link](http://www.careercup.com/question?id=12426697)

> Given a RNG r(5) which generates number between 1-5 uniformly, make r(7) which generates random number between 1-7. 

### Solution

    int rand7() {
        int r = 0;
        do {
            int a = rand(5) - 1;    //uniformly at random from 0 to 4
            int b = rand(5) - 1;
            r = 5 * b + a;            //uniformly at random from 0 to 24
        }
        while (r >= 21);            // in this event, we have to roll again
        return r % 7 + 1; 
    }
