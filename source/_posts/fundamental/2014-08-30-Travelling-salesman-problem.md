---
layout: post
title: "[Fundamental] Travelling salesman problem "
comments: true
category: Fundamental

---

### TSP problem

[Given a list of cities](http://en.wikipedia.org/wiki/Travelling_salesman_problem) and the distances between each pair of cities, what is the shortest possible route that visits each city exactly once and returns to the origin city? 

It is an NP-hard problem in combinatorial optimization. We will discuss 2 category of solutions: 

1. Exact algorithms
1. Heuristic and approximation algorithms

### Exact algorithms

1. __Brute force search__, which the run time is O(n!), which is impossible for 20 cities. 

1. __DP__ Held–Karp algorithm. O(n^2 x 2^n). 

1. __Branch-and-bound__ algorithm. This can process 40-60 cities. 

### Heuristic and approximation algorithms

1. __Greedy__, or Nearest Neighbour algorithm. (an improved version is called Nearest Fragment algorithm, which connect NN in groups)

1. __Minimum Spanning Tree (MST)__, build the [MST](http://en.m.wikipedia.org/wiki/Minimum_spanning_tree) using [Kruskal's algorithm](http://en.wikipedia.org/wiki/Kruskal's_algorithm) and then do a __Depth-first Tree Tour__. [link](http://www.youtube.com/watch?v=HWHZAtQl1vI) to video. 

	1. Sort all edges from small to large, then add edges into MST as long as no cycle is created. In the end, a MST is achieved. 
	
	1. Do Depth-first Tree Tour(DFTT)
	
	1. Length of DFTT is 2 x weight of MST.
	
	1. Skip some nodes that's only visited once. 

	1. We get an legitimate solution. 

### Iterative improvement

Now these are the solutions. However we can improve it by doing __2-opt Swap__. 

It means selecting 2 edges at random. If swapping results in an improvement, then keep it. Keep doing this. [link](http://www.youtube.com/watch?v=SC5CX8drAtU) to video. 
