---
layout: post
title: "[Palantir] MultiMap in Java without using Collections "
comments: true
category: Question

---

### Question 

[link](http://www.careercup.com/question?id=18479662)

> Explain how you would implement a multi-map in Java without using any collections?

### Solution

This question is pretty strange in a tech interview. But still, if you are asked, I think the most obvious solution is pointed out by [careercup user Abhi](http://www.careercup.com/question?id=18479662). 

The basic idea is to build a nested list structure ourselves, without considering the time complexity. See code below. 

### Code

    public class Node {
        Object key;
        Node next;
        ValueNode vnode;
    }
    public class ValueNode {
        Object Value;
        ValueNode next;
    }
