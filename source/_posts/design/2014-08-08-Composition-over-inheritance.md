---
layout: post
title: "[Design] Composition Over Inheritance"
comments: true
category: Design
---

### Overview

[Composition over inheritance](http://en.wikipedia.org/wiki/Composition_over_inheritance) in OOP is a technique by which classes achieve __polymorphic behavior and code reuse__ by containing other classes __instead of__ through inheritance. 

### Benefits

[It gives](http://en.wikipedia.org/wiki/Composition_over_inheritance#Benefits) the design __higher flexibility__, giving business-domain classes and more stable business domain in the long term. In other words, HAS-A can be better than an IS-A relationship.

__And inheritance [breaks encapsulation](http://stackoverflow.com/a/891908)__! This post also points out these (which is hard to understand): 

> 1. You can't change the implementation inherited from super classes at runtime (obviously because inheritance is defined at compile time).

> 1. Inheritance exposes a subclass to details of its parent's class implementation, that's why it's often said that inheritance breaks encapsulation (in a sense that you really need to focus on interfaces only not implementation, so reusing by sub classing is not always preferred).

> 1. The tight coupling provided by inheritance makes the implementation of a subclass very bound up with the implementation of a super class that any change in the parent implementation will force the sub class to change.

> 1. Excessive reusing by sub-classing can make the inheritance stack very deep and very confusing too.
