---
layout: post
title: "[Design] MapReduce Common Friends Example"
comments: true
category: Design

---

### Question

[link](http://stackoverflow.com/a/12375878)

> Facebook's "You and Joe have 230 friends in common" feature. Sure you could use a decent caching strategy, but for now, use MapReduce. 

### Analysis

This list doesn't change frequently so it'd be wasteful to recalculate it every time. We're going to use mapreduce to calculate everyone's common friends once a day and store those results.

Note that friends are __bi-directional__. If I'm your friend, you're mine. (follow-up: how to do it for follower system?)

#### Input

Assume the friends are stored as Person->[List of Friends], our friends list is then:

    A -> B C D
    B -> A C D E
    C -> A B D E
    D -> A B C E
    E -> B C D

#### Map

The mapper will output a key-value pair. The key will be a friend along with the person. The value will be the list of friends. The key will be sorted so that the friends are in order, causing all pairs of friends to go to the same reducer. 

For map(A -> B C D) :

    (A B) -> B C D
    (A C) -> B C D
    (A D) -> B C D

For map(B -> A C D E) : (Note that A comes before B in the key)

    (A B) -> A C D E
    (B C) -> A C D E
    (B D) -> A C D E
    (B E) -> A C D E

For map(C -> A B D E) :

    (A C) -> A B D E
    (B C) -> A B D E
    (C D) -> A B D E
    (C E) -> A B D E

For map(D -> A B C E) :

    (A D) -> A B C E
    (B D) -> A B C E
    (C D) -> A B C E
    (D E) -> A B C E

And finally for map(E -> B C D):

    (B E) -> B C D
    (C E) -> B C D
    (D E) -> B C D

Before we send these key-value pairs to the reducers, we group them by their keys and get:

    (A B) -> (A C D E) (B C D)
    (A C) -> (A B D E) (B C D)
    (A D) -> (A B C E) (B C D)
    (B C) -> (A B D E) (A C D E)
    (B D) -> (A B C E) (A C D E)
    (B E) -> (A C D E) (B C D)
    (C D) -> (A B C E) (A B D E)
    (C E) -> (A B D E) (B C D)
    (D E) -> (A B C E) (B C D)

Each line will be passed as an argument to a reducer.

#### Reduce

The reduce function will simply intersect the lists of values and output the same key with the result of the intersection. After reduction:

    (A B) -> (C D)
    (A C) -> (B D)
    (A D) -> (B C)
    (B C) -> (A D E)
    (B D) -> (A C E)
    (B E) -> (C D)
    (C D) -> (A B E)
    (C E) -> (B D)
    (D E) -> (B C)

#### Result

Now when D visits B's profile, we can quickly look up (B D) and see that they have three friends in common, (A C E). 
