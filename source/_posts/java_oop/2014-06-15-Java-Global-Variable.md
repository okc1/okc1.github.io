---
layout: post
title: "[Java OOP] Java Global Variable"
comments: true
category: Java OOP

---

### Global variable?

There is no such thing as a 'global variable' in Java. 

> In computer programming, a global variable is a variable that is accessible in every scope (the global environment). Some languages, like Java, don't have global variables. [reference](https://sg.answers.yahoo.com/question/index?qid=20110811104130AA5JrbR)

But static variable can be seen as one, although every static variable must belong to some class (like Math.MIN_VALUE). 

Global variables are generally only used for declaring constants. In this case, declare it as 'final static'. [reference](http://stackoverflow.com/questions/4646577/global-variables-in-java)

### Four types of variable in Java

#### Local variables 

Created when the method, constructor or block is entered and will be destroyed once it exits the method, constructor or block. 

#### Instance variables 

Outside a method or constructor. 

When a space is allocated for an object in the heap, a slot for each instance variable value is created. It is destroyed when the object is destroyed. 

#### Class/static variables

Static variable is class variable. 

Declared with 'static' keyword in a class. 

#### Constants

Most common usage of static variable - constant. 

Declared with 'static final' keyword in a class. 

### One more thing

About [stack and heap in Java](http://programmers.stackexchange.com/a/65289): 

> In Java, primitives are created on the stack. 
>
> Objects are created on the heap, and only references (which in turn are primitives) are passed around on the stack.
>
> If you create an object, it is put on the heap, with all the variables that belong to it, so that it can persist after the function call returns.
