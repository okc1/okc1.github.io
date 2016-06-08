---
layout: post
title: "[Question] Nth Fibonacci Number In O(LogN)"
comments: true
category: Question

---

### Question 

[link](http://tech-queries.blogspot.sg/2010/09/nth-fibbonacci-number-in-ologn.html)

> Find Nth fibonacci number in O(logN) time complexity.

### Solution

{% img middle /assets/images/fibonacci_matrix.png %}

It's a recursive sequence, where we can get the following equation: 

	A* [ F(1) F(0) ] = [ F(2) F(1) ]
	A* [ F(2) F(1) ] = [ F(3) F(2) ] = A^2 * [ F(1) F(0) ]
	A* [ F(3) F(2) ] = [ F(4) F(3) ] = A^3 * [ F(1) F(0) ]
	..
	..
	..
	..
	A* [ F(n) F(n-1) ] = [ F(n+1) F(n) ] = A^n * [ F(1) F(0) ]

Which means: 

{% img middle /assets/images/fibonacci_equation.png %}

So all that is left is finding the nth power of the matrix A. Well, this can be computed in O(log n) time, by recursive doubling. For more, see question post or [here](http://www.codechef.com/wiki/tutorial-dynamic-programming#Finding_nth_Finobacci_number_in_Olog_n). 

### Code

__not written__


