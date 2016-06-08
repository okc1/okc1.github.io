---
layout: post
title: "[Brain teaser] 2 Eggs 100 Floors Puzzle "
comments: true
category: Question

---


### Question 

[link](http://www.programmerinterview.com/index.php/puzzles/2-eggs-100-floors-puzzle/)

> You are given 2 eggs.
>
> You have access to a 100-storey building.
>
> Eggs can be very hard or very fragile means it may break if dropped from the first floor or may not even break if dropped from 100 th floor.Both eggs are identical.
>
> You need to figure out the highest floor of a 100-storey building an egg can be dropped without breaking.
>
> Now the question is how many drops you need to make. You are allowed to break 2 eggs in the process

### Analysis

Most obvious solutoin is drop in 10th, 20th, 30th ... floor. But this solution would result in __19 drops in worst case__. We should try to reduce the worst case scenario by making all possible scenarios take the same number of drops! 

The best solution is: 

> What if we tried to reduce the number of drops that would be required with the linear search (with the 2nd egg) after we get to one of the higher floors? This way we __counteract the fact that getting to the higher floor took so many drops__, and if we use less drops for the linear search we are __balancing out the worst case__. 

According to the [solution](http://www.programmerinterview.com/index.php/puzzles/2-eggs-100-floors-puzzle/), we form a series: 

> x + (x-1) + (x-2) + (x-3) + ... + 1 = 100
>
> x(x+1)/2 = 100
>
> x = 14

### Final Result

We would drop in this way: 

<table width="50">
<thead><tr><th>&nbsp;Drop&nbsp;</th><th>&nbsp;Floor&nbsp;</th></tr></thead>
<tbody><tr align="center"><td>#1</td><td>14</td></tr>
<tr align="center"><td>#2</td><td>27</td></tr>
<tr align="center"><td>#3</td><td>39</td></tr>
<tr align="center"><td>#4</td><td>50</td></tr>
<tr align="center"><td>#5</td><td>60</td></tr>
<tr align="center"><td>#6</td><td>69</td></tr>
<tr align="center"><td>#7</td><td>77</td></tr>
<tr align="center"><td>#8</td><td>84</td></tr>
<tr align="center"><td>#9</td><td>90</td></tr>
<tr align="center"><td>#10</td><td>95</td></tr>
<tr align="center"><td>#11</td><td>99</td></tr>
<tr align="center"><td>#12</td><td>100</td></tr>
</tbody>
</table>
