---
layout: post
title: "[Design] Time complexity calculation (Master theorem)"
comments: true
category: Design

---


### Master theorem

In the analysis of algorithms, the [master theorem](http://en.wikipedia.org/wiki/Master_theorem) provides a cookbook solution in asymptotic terms (using Big O notation) for recurrence relations that occur in many divide and conquer algorithms. It was introduced and popularized by __Introduction to Algorithms__. 

### Examples with common algorithms

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
</style>
<table class="tg">
  <tr>
    <th class="tg-031e">Algorithm</th>
    <th class="tg-031e">Recurrence</th>
    <th class="tg-031e">Big-Oh Solution</th>
  </tr>
  <tr>
    <td class="tg-031e">Binary Search</td>
    <td class="tg-031e">T(n) = T(n/2) + O(1)</td>
    <td class="tg-031e">O(log n)</td>
  </tr>
  <tr>
    <td class="tg-031e">tree traversal</td>
    <td class="tg-031e">T(n) = 2 T(n/2) + O(1)</td>
    <td class="tg-031e">O(n)</td>
  </tr>
  <tr>
    <td class="tg-031e">Mergesort</td>
    <td class="tg-031e">T(n) = 2 T(n/2) + O(n)</td>
    <td class="tg-031e">O(n log n)</td>
  </tr>
</table>

[source](http://www.cs.duke.edu/~ola/ap/recurrence.html)
