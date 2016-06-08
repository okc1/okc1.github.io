---
layout: post
title: "[Design] HashMap vs Hashtable vs HashSet"
comments: true
category: Design
tags: [ General ]
---

## Overview

### HashTable

1. HashTable is thread safe synchronized. Only 1 thread can access at a time (compromise speed). 
1. HashTable does not allow null for key and value. 

### HashMap & HashSet

1. HashMap is not sync, but better performance. 
1. HashMap allows null key or null value. 
1. HashSet is same as HashMap, just interface difference. 

## Conclusion

1. HashMap is roughly equivalent to Hashtable, except that it is unsynchronized and permits nulls. 
1. HashSet is same as HashMap. It's not thread safe. 

### Implementation

1. C++ Map is rbtree
1. Java HashMap is buckets + entries (using Array + LinkedList)
1. HashTable in Java is basically HashMap + lock

### One more thing

HashMap is locked-out during rehashing, so it's better to avoid rehashing (by setting initial size bigger).
