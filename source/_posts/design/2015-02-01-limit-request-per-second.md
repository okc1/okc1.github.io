---
layout: post
title: "[Design] Limit the Request per Second "
comments: true
category: Design

---

### Question

[link](http://www.mitbbs.com/article_t/JobHunting/32841633.html)

> 有一个接口叫 void setRPS(int num);

> 接下来不断有request过来，如何实现下面的接口，返回accept或者deny，

    bool process(int timestamp){
    
    }

### Solution

Suggested by level 5 of [this post](http://www.mitbbs.com/article_t/JobHunting/32841633.html):

1. maintain a variable for the number of request processed/rejected.
    1. This variable must be atomic, thus a __AtomicInteger__. 
    1. the variable is called 'count'
1. have a method to process request
    1. if count < limit, do it
    1. otherwise, reject
1. __This is the most important__: clear the count every 1 seconds! 
    1. eg. LIMIT = 5r/s, so: 
    1. the __first 5 number of requests in every second__ are getting fulfilled
    1. from 6th request onward, the request all rejected, until the next second.

### Code 

    public class SetRps {

        AtomicInteger count = new AtomicInteger(0);
        int limit = -1;
        int printIndex = 1;
        long startTimestamp = -1;

        void setRPS(int num) {
            limit = num;
        }

        boolean process(long timestamp) {
            // suppose timestamp is ms
            synchronized (this) {
                // to process or not to process
                if (count.get() < limit) {
                    // can process
                    count.incrementAndGet();
                    System.out.println(printIndex++ + ". processing request "
                            + timestamp % 100000 / 1000 + "," + timestamp % 1000);
                    return true;
                }
                // to clear or not to clear
                if (timestamp - startTimestamp >= 1000) {
                    // every 1 seconds, reset
                    count.set(0);
                    startTimestamp = timestamp;
                    System.out.println("clear!");
                    return true;
                }
            }
            return false;
        }
    }
