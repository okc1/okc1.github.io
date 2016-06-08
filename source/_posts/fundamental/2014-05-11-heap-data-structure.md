---
layout: post
title: "[Fundamental] Heap (data structure) "
comments: true
category: Fundamental

---

### Definition

[A heap](http://en.wikipedia.org/wiki/Heap_%28data_structure%29) is a specialized tree-based data structure that satisfies the heap property: 

> If A is a parent node of B, then the key of node A is ordered with respect to the key of node B with the same ordering applying across the heap. 

Heaps can then be classified further as either "max heap" and "min heap". 

### Details

> We take max heap for example. The keys of parent nodes are always greater than or equal to the children node. 
>
> __The heap is an implementation of priority queue__. In fact, priority queues are often referred to as "heaps", regardless of how they may be implemented. 
>
> Note that despite the similarity of the name "heap" to "stack" and "queue", the latter two are __abstract data types__, while a heap is a __specific data structure__, and "priority queue" is the proper term for the abstract data type. 

#### Insert

1. Add the element to the bottom level of the heap.

1. Compare the added element with its parent; if they are in the correct order, stop.

1. If not, swap the element with its parent and return to the previous step.

The number of operations required is dependent on the __number of levels__ the new element must rise to satisfy the heap property, thus the insertion operation has a time complexity of O(log n).

#### Delete

1. Replace the root of the heap with the last element on the last level.

1. Compare the new root with its children; if they are in the correct order, stop.

1. If not, swap the element with one of its children and return to the previous step. (Swap with its smaller child in a min-heap and its larger child in a max-heap.)

### Time complexity

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg .tg-s6z2{text-align:center}
</style>
<table class="tg">
  <tr>
    <th class="tg-s6z2">Heap</th>
    <th class="tg-s6z2">Time</th>
  </tr>
  <tr>
    <td class="tg-031e">Find max</td>
    <td class="tg-s6z2">O(1)</td>
  </tr>
  <tr>
    <td class="tg-031e">Delete</td>
    <td class="tg-s6z2">O(lgn)</td>
  </tr>
  <tr>
    <td class="tg-031e">Insert</td>
    <td class="tg-s6z2">O(lgn)</td>
  </tr>
  <tr>
    <td class="tg-031e">Merge</td>
    <td class="tg-s6z2">O(n)</td>
  </tr>
</table>
<br />

#### How about building a heap? 

It's [O(n)](http://en.wikipedia.org/wiki/Binary_heap#Building_a_heap). 

Why? You may ask - "why not O(nlgn) like we do successive insert for n time"?

Read answers from [stackoverflow](http://stackoverflow.com/questions/9755721/build-heap-complexity). 
