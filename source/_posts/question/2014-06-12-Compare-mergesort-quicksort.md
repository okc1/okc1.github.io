---
layout: post
title: "[Question] Compare Mergesort and Quicksort"
category: Question

---


### Quicksort

__Quicksort is faster__ because it's in-place sort (with O(log n) stack space). 

Typical in-place sort is not stable. 

### Mergesort

Mergesort uses O(n) space, thus slower. 

It is stable sort. 

### Stability 稳定排序

When sorting, if only part of the data is examined, there're possibility of multiple different correctly sorted versions of the original list. Stable sorting algorithms will preserve the original relative order.

One application for stable sorting algorithms is sorting a list using a primary and secondary key.

Example: 

{% img middle /assets/images/sort-stability.png %}

Stable sort: first sorting by rank/number (using any sort), and then a stable sort by suit. 

Quicksort would not be able to do that. 

### Conclusion

Quicksort is faster. 

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
</style>
<table class="tg">
  <tr>
    <th class="tg-031e"></th>
    <th class="tg-031e">Best</th>
    <th class="tg-031e">Average</th>
    <th class="tg-031e">Worst</th>
    <th class="tg-031e">Memory</th>
    <th class="tg-031e">Stability</th>
  </tr>
  <tr>
    <td class="tg-031e">Quicksort</td>
    <td class="tg-031e">nlgn</td>
    <td class="tg-031e">nlgn</td>
    <td class="tg-031e">n^2</td>
    <td class="tg-031e">lgn average<br>n worst case</td>
    <td class="tg-031e">Not</td>
  </tr>
  <tr>
    <td class="tg-031e">Merge sort</td>
    <td class="tg-031e">nlgn</td>
    <td class="tg-031e">nlgn</td>
    <td class="tg-031e">nlgn</td>
    <td class="tg-031e">n worst case</td>
    <td class="tg-031e">Yes</td>
  </tr>
</table>
