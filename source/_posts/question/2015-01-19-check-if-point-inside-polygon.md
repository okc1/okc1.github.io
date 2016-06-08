---
layout: post
title: "[Question] Check if given point inside polygon "
comments: true
category: Question

---

### Question

[link](http://www.geeksforgeeks.org/how-to-check-if-a-given-point-lies-inside-a-polygon/)

> Given a polygon and a point ‘p’, find if ‘p’ lies inside the polygon or not. The points lying on the border are considered inside.

{% img middle /assets/images/point-in-polygon.png %}

### Solution

Prerequisite reading: __[Question] Check if two line segments intersect__. 

Suggested by G4G, this is a simple idea to check:

{% img middle /assets/images/polygon31-300x169.png %}

1. Draw a horizontal line to the right of each point and extend it to infinity

1. Count the number of times the line intersects with polygon edges.

1. A point is inside the polygon if either count of intersections is odd or point lies on an edge of polygon. 

1. Note the special case of point 'g'. 
