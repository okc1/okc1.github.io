---
layout: post
title: "[Design] DFS, BFS and space efficiency"
comments: true
category: Design

---


### First Word

This post talks about BFS, DFS and space efficiency. 

### Analysis

__For BFS__ it's easy to understand. It is implemented with a queue. __Space usage is O(width)__

__For DFS__, there are 2 types: true DFS and pseudo-DFS. True DFS space usage is __O(depth)__, while psudo-DFS is __O(depth x [branching factor](http://en.wikipedia.org/wiki/Branching_factor))__. 

> __branching factor__ is the number of children at each node, the outdegree. 

Pseudo-DFS is implemented by __simply take the BFS implementation and replace the Queue with Stack__. But true-DFS is a very different algorithm where the __stack is use for backtracking only__. [This](http://stackoverflow.com/a/20429574) is a great article talking about this topic. 

> the true classic DFS cannot be obtained from BFS by such queue-to-stack replacement. The classic DFS is a completely different algorithm with significantly different inner structure. True DFS is a genuinely recursive algorithm that uses stack for backtracking purposes, not for storing the vertex discovery "front" (as is the case in BFS)

__The following quoted texts are also worth-reading__.

> Something worth noting - Pseudo-DFS should give you O(depth * branching factor) space, as opposed to O(depth) for proper DFS, which is still better than O(width). 

> The defining characteristic that separates true DFS and what you call pseudo DFS is how they use the stack. True DFS use it to store backtracking information in contrast to pseudo DFS which used the stack to store the vertex discovery front.

### Examples

__Given a perfect binary search tree of 4 levels__. BFS would require 8 space, while DFS requires only 4 space. The branching factor is 2, so true and pseudo DFS use same amount of space. 

__Given a star graph__: a single central vertex surrounded by 1000 peripheral vertices, with each connected to the central vertex. If we run BFS on this graph, the queue size will immediately jump to 1000. The same thing happens for pseudo-DFS. But classic DFS algorithm will need stack depth of only 1 (!) to traverse this entire graph. 

