---
layout: post
title: "[Google] Make a Java method thread-safe "
comments: true
category: q-google

---

### Question 

[link](http://www.programcreek.com/2014/02/how-to-make-a-method-thread-safe-in-java/)

> Consider the following class: 

    class MyCounter {
        private static int counter = 0;

        public static int getCount() {
            return counter++;
        }
    }

> Is the method thread-safe? How to make it thread-safe?

### Solution 

__No__, it's not. 

> The method is not thread-safe, because the __counter++ operation is not atomic__, which means it consists more than one atomic operations. In this case, one is accessing value and the other is increasing the value by one.

> When Thread 1 accesses the method at t1, Thread 2 may not be done with the method. So the value returned to Thread 1 is the value that has not been increased.

### Approach 1

Adding __synchronized__ to this method. This will synchronize the instance of the static class. 

    class MyCounter {
        private static int counter = 0;

        public static synchronized int getCount() {
            return counter++;
        }
    }

### Approach 2

We actually can make __count++__ atomic by using AtomicInteger from the package "java.util.concurrent.atomic". 

import java.util.concurrent.atomic.AtomicInteger;
 
    public class MyCounter {
        private static AtomicInteger counter = new AtomicInteger(0);

        public static int getCount() {
            return counter.getAndIncrement();
        }
    }

### Follow-up on thread stack

1. Each thread has its own stack (never share stack). 
1. All local variables defined in a method will be allocated memory in stack. 
1. When execution completed by a thread, stack frame will be removed.
