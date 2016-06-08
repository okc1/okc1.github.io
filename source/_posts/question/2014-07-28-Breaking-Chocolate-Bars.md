---
layout: post
title: "[Question] Breaking Chocolate Bars "
comments: true
category: Question

---

### Game #1

[link](http://www.cut-the-knot.org/proofs/chocolad.shtml)

> Two players take turns breaking a chacolate bar (rectangle-shaped consist of squares). The last to break a piece wins the game. 

> Design the strategy. 

#### Solution

Each time the bar is broken, __total number of pieces increase by 1__. Suppose there're even number of squares, 1st player wins regardless of breaking strategy. And vice versa. 

### Problem #2

[link](http://www.cut-the-knot.org/proofs/chocolad.shtml)

> 75 teams took part in a competition where teams met 1-on-1. Each time the defeated team drops out. 

> How many meets are needed to before one team is declared a winner?

#### Solution

Each game will eliminate 1 game, so it needs 74 games. 

### Splitting Piles

[link](http://www.cut-the-knot.org/arithmetic/rapid/piles.shtml)

> Given a random number of items in a pile. Ask an audience to split a pile into two piles, multiply the numbers of items in the two new piles and keep adding the results. The process stops when there is no pile with more than 1 chip.

> For example, let start with 9 chips:

<table cellpadding="10">
<tbody><tr><td align="center">Piles</td><td align="center">Which is broken</td><td align="center">What's added</td><td align="center">Total</td></tr>
<tr><td colspan="4"><hr></td></tr>
<tr><td align="center">9</td><td align="center">9</td><td align="center">3*6</td><td align="center">18</td></tr>
<tr><td align="center">3,6</td><td align="center">3</td><td align="center">1*2</td><td align="center">20</td></tr>
<tr><td align="center">1,2,6</td><td align="center">6</td><td align="center">3*3</td><td align="center">29</td></tr>
<tr><td align="center">1,2,3,3</td><td align="center">3</td><td align="center">1*2</td><td align="center">31</td></tr>
<tr><td align="center">1,2,1,2,3</td><td align="center">2</td><td align="center">1*1</td><td align="center">32</td></tr>
<tr><td align="center">1,1,1,1,2,3</td><td align="center">2</td><td align="center">1*1</td><td align="center">33</td></tr>
<tr><td align="center">1,1,1,1,1,1,3</td><td align="center">3</td><td align="center">1*2</td><td align="center">35</td></tr>
<tr><td align="center">1,1,1,1,1,1,1,2</td><td align="center">2</td><td align="center">1*1</td><td align="center"><b>36</b></td></tr>
<tr><td align="center">1,1,1,1,1,1,1,1,1</td><td align="center">-</td><td align="center">-</td><td align="center">-</td></tr>
</tbody></table>

> Before the audience told the final number, you immediately guess it's 36. How did you do it? 

#### Solution

The result does not depend on how the piles are split; but only on the initial size of the very first pile. __Answer is always N(N - 1)/2__.

This can be proved by [mathematical induction](http://www.cut-the-knot.org/arithmetic/rapid/piles.shtml). 
