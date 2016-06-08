---
layout: post
title: "[Fundamental] Min-Max Algorithm (minmax) "
comments: true
category: Fundamental

---

### Definition

For every two-person, zero-sum game with finitely many strategies, there exists a value V and a mixed strategy for each player, such that

1. Given player 2's strategy, the best payoff possible for player 1 is V, and
1. Given player 1's strategy, the best payoff possible for player 2 is −V.

Equivalently, Player 1's strategy guarantees him a payoff of V regardless of Player 2's strategy. 

Put it in a simple way: MAX tries to __max the utility__, and MIN try to __min it__. 

{% img middle /assets/images/minmax-example-1.png %}

### Steps

1. Have a __heuristic evaluation function__, which gives a value to non-final game states. 
1. Generate the values down to terminal states. 
1. Min-max calculate the utility, like this: 

{% img middle /assets/images/minmax-example-2.png %}

### An example

Othello game:

> A player can place a new piece in a position if there exists at least one straight (horizontal, vertical, or diagonal) occupied line between the new piece and another piece of the same kind, with one or more contiguous pieces from the opponent player between them. 
>
> After placing the new piece, the pieces from the opponent player will be captured and become the pieces from the same player. 
>
> The player with the most pieces on the board wins. 

First, the __heuristic evaluation function__:

{% img middle /assets/images/minmax-example-2.png %}

Now, generate terminal level utility values: 

{% img middle /assets/images/minmax-example-3.png %}

Now, do min-max algorithm: 

{% img middle /assets/images/minmax-example-4.png %}

### Pruning

The performance of the naïve minimax algorithm may be improved dramatically, without affecting the result, [by the use of](http://en.wikipedia.org/wiki/Minimax#Minimax_algorithm_with_alternate_moves) __alpha-beta pruning__. 

[Alpha–beta pruning](http://en.wikipedia.org/wiki/Alpha%E2%80%93beta_pruning) is a search algorithm that seeks to decrease the number of nodes that are evaluated by the minimax algorithm in its search tree. 

{% img middle /assets/images/minmax-ab-pruning.png %}

It works when you evaluate the tree __left-to-rigth__. Considering under the same parent, once you found any number that is largest then the smallest-found-so-far, in the MAX level, you can skip this node. Example: 

{% img middle /assets/images/minmax-ab-pruning2.png %}

The pruned values won't influence the final result.
