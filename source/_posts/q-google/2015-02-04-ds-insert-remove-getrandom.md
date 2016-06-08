---
layout: post
title: "[Google] Data Structure of Insert, Remove, GetRandom "
comments: true
category: q-google

---

### Question 

[link](http://www.careercup.com/question?id=11353907)

> Design a data structure where the following 3 functions at O(1): 

    1. Insert(n) 
    2. GetRandomElement() 
    3. Remove(n) 

### Solution

Array is best for: 

1. random access

HashMap is best for: 

1. Searching
    1. insert
    1. remove

[So the answer is](http://stackoverflow.com/a/22083895) __array + hashmap__: 

1. Insertion can be done by appending to the array and adding to the hash-map.

1. Deletion can be done by first looking up and removing the array index in the hash-map, then __swapping the last element with that element in the array__. 

1. Get random can be done by returning a random index from the array.

1. All operations take O(1).

Note [how hashmap is used](http://stackoverflow.com/a/5684892):

> insert(value): append the value to array and let i be it's index in A. Set H[value]=i.

Hashmap stores value's index in the array - that is to say: __this DS does not support inserting duplicating values__. 

Finally, when we delete, we swap the last element to replace the gap. This is an nice idea! 

#### follow-up

> what if we want to get the top x% number?

Well, heap of course. And note that __Heap size is [auto-increasing](http://stackoverflow.com/a/9115884)__: 

> PriorityQueue is unbounded, it can grow as big as your memory allows, and it will grow automatically when needed. The initialCapacity parameter is just a hint to reserve room for that many elements initially.
