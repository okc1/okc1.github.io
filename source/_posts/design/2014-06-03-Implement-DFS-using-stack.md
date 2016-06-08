---
layout: post
title: "[Design] Implemention of DFS using a Stack"
comments: true
category: Design

---


### First Word

This post talks about how to implement DFS without recursion. 

We have studied 2 kinds of DFS in the post __DFS, BFS and space efficiency__. We will skip "true DFS" here, and only talk about "pseudo-DFS" implementation. 

Remember, __space usage of psudo-DFS is O(depth x branching factor)__. 

### Analysis

A DFS without recursion is basically the same as BFS - but use a stack instead of a queue as the data structure. 

More details are discussed in [this thread](http://stackoverflow.com/questions/21508765/how-to-implement-depth-first-search-for-graph-with-non-recursive-aprroach). 

### Implementation

The following code come from [this post](http://stackoverflow.com/a/21508819).

    DFS(source):
      s <- new stack
      visited <- {} //empty set
      s.push(source)
      while (s.empty() == false):
        current <- s.pop()
        if (current is in visited):
            continue
        visited.add(current)
        //do something with current
        for each node v such that (source,v) is an edge:
            s.push(v)
