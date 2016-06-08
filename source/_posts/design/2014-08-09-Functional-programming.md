---
layout: post
title: "[Design] Functional programming"
comments: true
category: Design

---

### Overview

__[A functional language](http://stackoverflow.com/a/23290) allows you to write a mathematical function__, i.e. a function that takes n arguments and returns a value. If the program is executed, this function is evaluated. 

A purely functional program __always yields the same value for an input__, and the order of evaluation is not well-defined; which means that uncertain values like user input or random values are hard to model in purely functional languages. 

### One Sentence

__Functional programming is like describing your [problem to a mathematician](http://stackoverflow.com/a/23475). Imperative programming is like giving instructions to an idiot__. 

### Pros and Cons

Functional Programming allows coding [with fewer potentials for bugs](http://stackoverflow.com/a/24294) because each component is completely isolated. Also, using recursion and first-class functions allows for __simple proofs of correctness__ which typically mirror the structure of the code.

Functional programming languages are typically [less efficient](http://en.wikipedia.org/wiki/Functional_programming#Efficiency_issues) in their use of CPU and memory than imperative languages such as C and Pascal.
