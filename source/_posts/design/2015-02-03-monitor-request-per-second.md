---
layout: post
title: "[Design] Monitor Rps for Past sec/min/hr "
comments: true
category: Design

---

### Question

[link](http://www.careercup.com/question?id=6005446611566592)

> Given a server that has requests coming in. 

> Design a data structure such that you can fetch the count of the number requests in the last second, minute and hour.

### Solution 1

__Keep a record of all request timestamps__, suggested by the top answer by [whatevva](http://www.careercup.com/question?id=6005446611566592): 

1. Use a queue implemented as a resizable array to store the timestamps of all new requests 

1. maintain head/tail pointers as usual 

1. Also maintain three pointers, for past sec, past min and past hr. 

Whenever a request comes in, update 3 pointers. Then in the for-loop of the thread, remove old entries and also update 3 pointers. 

Print Rps in real time. I posted my code below (the code is without thread-safety consideration).

### Solution 2

This solution does not store all timestamps, and it does not generate real-time Rps data. But it's good enough because result is only updated every 1 second, so its performance is better. 

Keep an array of int of size 60 * 60. Each second, use the __number of request in the past second__ to update the array values __in a rolling way__. 

### Code 

Solution 1. this is my code so please correct me! 

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
                if (count.get() < limit) {
                    // can process
                    count.incrementAndGet();
                    System.out.println(printIndex++ + ". processing request "
                            + timestamp % 100000 / 1000 + "," + timestamp % 1000);
                    return true;
                }
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
