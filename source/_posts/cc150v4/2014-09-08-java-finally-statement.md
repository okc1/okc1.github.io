---
layout: post
title: "[CC150v4] 14.2 Java Finally Statement "
comments: true
categories:
- CC150v4
- Java OOP

---

### Question

> In Java, does the finally block gets executed if we insert a return statement inside the try block of a try-catch-finally?

### Solution

Yes, it will.

Even when we attempt to exit within the try block (normal exit, return, continue, break or any exception), __the finally block will still be executed__. 

The only time finally [won't be called](http://stackoverflow.com/a/65049) is if you call System.exit() or if the JVM crashes first.
