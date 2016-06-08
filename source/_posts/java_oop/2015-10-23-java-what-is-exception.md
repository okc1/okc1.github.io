---
layout: post
title: "[Java OOP] What is Java Exception"
category: Java OOP

---

# The class

__[The class Exception](http://docs.oracle.com/javase/7/docs/api/java/lang/Exception.html)__ and its subclasses are a form of __Throwable__ that indicates conditions that a reasonable application might want to catch.

# The object

__[An exception is an event](https://docs.oracle.com/javase/tutorial/essential/exceptions/definition.html)__, which occurs during the execution of a program, that disrupts the normal flow of the program's instructions.

__When an error occurs__ within a method, the method __creates an object and hands it off to the runtime system__. The object, called an __exception object__, contains information about the error(eg. type, state etc). 

## throw this object out!

Creating an exception object and handing it to the runtime system is called __throwing an exception__.

After a method throws an exception, the runtime system (i.e. __JVM__) attempts to find something to handle it. This is __exception handler__.

