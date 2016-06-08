---
layout: post
title: "[Question] Packing Rectangles "
comments: true
category: Question

---

### Question 

[link](http://olympiads.win.tue.nl/ioi95/task/pack.html)

> Four rectangles are given. Find the smallest enclosing (new) rectangle into which these four may be fitted without overlapping. By smallest rectangle we mean the one with the smallest area.

{% img middle /assets/images/packing-rect.gif %}

### Greedy 

[Greedy](http://stackoverflow.com/a/1213571) placement from __large (area) to small__.

1. Put the largest rectangle remaining into your packed area. 
1. If it can't fit anywhere, place it in a place that extends the pack region as little as possible. 
1. Repeat until you finish with the smallest rectangle.

### Optimal Solution

[There is a trade-off](http://stackoverflow.com/a/4264497) between implementation complexity/time and optimality, but there is a wide range of algorithms to choose from.

Below is quoted: 

<blockquote>
    <div class="post-text" itemprop="text">
<ol>
<li><p>First-Fit Decreasing Height (FFDH) algorithm<br>
FFDH packs the next item R (in non-increasing height) on the first level where R fits. If no level can accommodate R, a new level is created.<br>
Time complexity of FFDH: O(n·log n).<br>
Approximation ratio: FFDH(I)&lt;=(17/10)·OPT(I)+1; the asymptotic bound of 17/10 is tight.</p></li>
<li><p>Next-Fit Decreasing Height (NFDH) algorithm<br>
NFDH packs the next item R (in non-increasing height) on the current level if R fits. Otherwise, the current level is "closed" and a new level is created.<br>
Time complexity: O(n·log n).<br>
Approximation ratio: NFDH(I) &lt;= 2·OPT(I)+1; the asymptotic bound of 2 is tight.</p></li>
<li><p>Best-Fit Decreasing Height (BFDH) algorithm<br>
BFDH packs the next item R (in non-increasing height) on the level, among those that can accommodate R, for which the residual horizontal space is the minimum. If no level can accommodate R, a new level is created. </p></li>
<li><p>Bottom-Left (BL) Algorithm<br>
BL first order items by non-increasing width. BL packs the next item as near to the bottom as it will fit and then as close to the left as it can go without overlapping with any packed item. Note that BL is not a level-oriented packing algorithm.<br>
Time complexity: O(n^2).<br>
Approximation ratio: BL(I) &lt;= 3·OPT(I).  </p></li>
<li><p>Baker's Up-Down (UD) algorithm<br>
UD uses a combination of BL and a generalization of NFDH. The width of the strip and the items are normalized so that the strip is of unit width. UD orders the items in non-increasing width and then divides the items into five groups, each with width in the range (1/2, 1], (1/3,1/2], (1/4,1/3], (1/5,1/4], (0,1/5]. The strip is also divided into five regions R1, ··· , R5. Basically, some items of width in the range (1/i+1, 1/i], for 1 &lt;= i &lt;= 4, are packed to region Ri by BL. Since BL leaves a space of increasing width from top to bottom at the right side of the strip, UD takes this advantage by first packing the item to Rj for j = 1, ··· , 4 (in order) from top to bottom. If there is no such space, the item is packed to Ri by BL. Finally, items of size at most 1/5 are packed to the spaces in R1, ··· , R4 by the (generalized) NFDH algorithm. Again if there is no space in these regions, the item is packed to R5 using NFDH.<br>
Approximation ratio: UD(I) &lt;= (5/4) · OPT(I)+(53/8)H, where H is the maximum height of the items; the asymptotic bound of 5/4 is tight.</p></li>
<li><p>Reverse-fit (RF) algorithm<br>
RF also normalizes the width of the strip and the items so that the strip is of unit width. RF first stacks all items of width greater than 1/2. Remaining items are sorted in non-increasing height and will be packed above the height H0 reached by those greater than 1/2. Then RF repeats the following process. Roughly speaking, RF packs items from left to right with their bottom along the line of height H0 until there is no more room. Then packs items from right to left and from top to bottom (called reverse-level) until the total width is at least 1/2. Then the reverse-level is dropped down until (at least) one of them touches some item below. The drop down is somehow repeated.<br>
Approximation ratio: RF(I) &lt;= 2·OPT(I).</p></li>
<li><p>Steinberg's algorithm<br>
Steinberg's algorithm, denoted as M in the paper, estimates an upper bound of the height H required to pack all the items such that it is proved that the input items can be packed into a rectangle of width W and height H. They then define seven procedures (with seven conditions), each to divide a problem into two smaller ones and solve them recursively. It has been showed that any tractable problem satisfies one of the seven conditions.<br>
Approximation ratio: M(I) &lt;= 2·OPT(I).</p></li>
<li><p>Split-Fit algorithm (SF)
SF divides items into two groups, L1 with width greater than 1/2 and L2 at most 1/2. All items of L1 are first packed by FFDH. Then they are arranged so that all items with width more than 2/3 are below those with width at most 2/3. This creates a rectangle R of space with width 1/3. Remaining items in L2 are then packed to R and the space above those packed with L1 using FFDH. The levels created in R are considered to be below those created above the packing of L1.<br>
Approximation ratio: SF(I) &lt;= (3/2) ·OPT(I) + 2; the asymptotic bound of 3/2 is tight.</p></li>
<li><p>Sleator's algorithm<br>
Sleater's algorithm consists of four steps:</p>

<ol>
<li><p>All items of width greater than 1/2 are packed on top of one another in the bottom of the strip. Suppose h0 is the height of the resulting packing All subsequent packing will occur above h0.</p></li>
<li><p>Remaining items are ordered by non-increasing height. A level of items are packed (in non-increasing height order) from left to right along the line of height h0. </p></li>
<li><p>A vertical line is then drawn in the middle to cut the strip into two equal halves (note this line may cut an item that is packed partially in the right half). Draw two horizontal line segments of length one half, one across the left half (called the left baseline) and one across the right half (called the right baseline) as low as possible such that the two lines do not cross any item.</p></li>
<li><p>Choose the left or right baseline which is of a lower height and pack a level of items into the corresponding half of the strip until the next item is too wide.</p></li>
</ol>

<p>A new baseline is formed and Step (4) is repeated on the lower baseline until all items are packed.<br>
Time complexity: O(n ·log n).<br>
The approximation ratio of Sleator's algorithm is 2.5 which is tight.</p></li>
</ol>
    </div>
</blockquote>

