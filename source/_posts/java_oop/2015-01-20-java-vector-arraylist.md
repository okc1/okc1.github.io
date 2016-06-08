---
layout: post
title: "[Java OOP] Java Vector and ArrayList "
comments: true
category: Java OOP

---

### Difference

1. Vectors are synchronized, ArrayLists are not.

1. Data Growth Methods

    [A Vector defaults to](http://stackoverflow.com/a/2986307) doubling the size of its array, while the ArrayList increases its array size by 50 percent.

### Similarities

1. Both Vector and ArrayList use __growable array__ data structure.

1. They both are __ordered collection classes__ as they maintain the elements insertion order.

1. Vector & ArrayList both allows duplicate and null values.

1. They both grows and shrinks automatically when overflow and deletion happens.

[source](http://beginnersbook.com/2013/12/difference-between-arraylist-and-vector-in-java/)

### History

The vector was not the part of collection framework - it has been included in collections later. It can be considered as __Legacy code__. 

__There is nothing about Vector which List collection cannot do__. Therefore Vector should be avoided. If there is a need of thread-safe operation, make ArrayList synchronized. 
