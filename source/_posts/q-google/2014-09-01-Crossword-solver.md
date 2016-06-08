---
layout: post
title: "[Google] Crosswod Solver"
comments: true
category: q-google

---

### Question 

[link](http://stackoverflow.com/questions/8585090/algorithm-for-crossword-puzzle-with-given-grid)

> Given a wordlist like this:

    1. ccaa
    1. baca
    1. baaa
    1. bbbb

> and a Grid like this: 

    X X 
    XXXX
    X X 
    XXXX

> Now solve this crossword. One possible solution: 

    b c 
    baca
    b a 
    baaa

### Solution

[The corssword problem](http://stackoverflow.com/a/8586102) is NP-Complete, so your best shot is brute force: just try all possibilities, and stop when a possibility is a valid. Return failure when you exhausted all possible solutions.

### Code

__Pseudo code for brute force__. (this just serve as a guide, not a complete/correct solution)

    solve(words,grid):
       if words is empty:
           if grid.isValudSol():
              return grid
           else:
              return None
       for each word in words:
           possibleSol <- grid.fillFirst(word)
           ret <- solve(words\{word},possibleSol)
           if (ret != None):
              return ret
       return None
