---
layout: post
title: "[Design] Merits of BST over HashTables"
comments: true
category: Design

---

### Question 

[What are the advantages](http://stackoverflow.com/questions/4128546/advantages-of-binary-search-trees-over-hash-tables) of binary search trees over hash tables? 

### Answer

1. __More memory-efficient__. (They do not reserve more memory than they need to)

    For instance, if a hash function has a range R(h) = 0...100, then you need to allocate an array of 100 (pointers-to) elements, even if you are just hashing 20 elements. 

1. [Inorder traverse](http://stackoverflow.com/a/4128585). 

1. Collision might hamper HashMap's performance. 

1. [Resizing issue](http://stackoverflow.com/a/4129272)

    When the hash table pressure grows too much, you often tend to enlargen and reallocate the hash table. The BST has simpler behavior here and does not tend to suddenly allocate a lot of data and do a rehashing operation. 

1. Binary search tree do range searches efficiently.

### One more thing

__Trees tend to be the [ultimate average data structure](http://stackoverflow.com/a/19896875)__. They can act as lists, can easily be split for parallel operation, have fast removal, insertion and lookup on the order of O(lgn). They do nothing particularly well, but they don't have any excessively bad behavior either. 
