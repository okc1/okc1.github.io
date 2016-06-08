---
layout: post
title: "[Java OOP] Java Vector and ArrayList "
comments: true
category: Java OOP

---

# Vector in Java

Vector class implements a __growable array__ of objects. 

It's an array, __not a list__. 

# Vector VS ArrayList

1. Vectors are synchronized, ArrayLists are not.
1. Data Growth Methods (ArrayList grow by 1/2 of its size, while Vector doubles)

Usage: [ALWAYS use ArrayLists](http://stackoverflow.com/a/2986307)

> The vector was not the part of collection framework, it has been included in collections later. __It can be considered as Legacy code__. 
>
> There is nothing about Vector which List collection cannot do. Therefore Vector __[should be avoided](http://beginnersbook.com/2013/12/difference-between-arraylist-and-vector-in-java/)__.
