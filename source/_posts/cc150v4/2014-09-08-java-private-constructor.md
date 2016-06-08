---
layout: post
title: "[CC150v4] 14.1 Java Private Constructor "
comments: true
categories:
- CC150v4
- Java OOP

---

### Question

> In terms of inheritance, what is the effect of keeping a constructor private? 

### Solution

[If the programmer](http://www.javapractices.com/topic/TopicAction.do?Id=40) does not provide a constructor for a class, __the system will always provide a default, public no-argument constructor__. 

To disable this default constructor, simply add a private no-argument constructor to the class. 

Two categories of usage: 

1. Object construction is entirely forbidden
	1. class offers only static members (sometimes called __[utility class](http://stackoverflow.com/a/17342889)__) 
1. Object construction is private only
	1. a class needs to prevent the caller from creating objects, like Singleton
