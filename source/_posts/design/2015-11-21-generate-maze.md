---
layout: post
title: "[Design] How to generate Maze "
comments: true
category: Design

---

# Question

[link](http://www.glassdoor.com/Interview/Design-a-2D-dungeon-crawling-game-It-must-allow-for-various-items-in-the-maze-walls-objects-and-computer-controlled-c-QTN_57.htm)

> Design a 2D dungeon crawling game. It must allow for   various items in the maze - walls, objects, and computer-controlled characters.

# Part 1: API design

Serialize:

> [if a certain cell has a wall](http://qr.ae/RbRhHv) to the North and West but not to the South or East, it would be represented as 1001, or 9... (e.g., "9,6,11,12\n3,10,10,4\n13,9,12,5\n3,6,1,6" in a 4x4 maze)

Design API~

# Part 2: Algorithm

## Depth-first search 

This is most common and [one of the simplest ways to generate a maze using a computer](https://en.wikipedia.org/wiki/Maze_generation_algorithm#Depth-first_search). It's commonly implemented using __[Recursive backtrack](https://en.wikipedia.org/wiki/Maze_generation_algorithm#Recursive_backtracker)__. 

1. from a random cell, select a random neighbour that hasn't been visited. 

1. removes the 'wall' and adds the new cell to a stack. 

1. a cell with no unvisited neighbours is considered __dead-end__. 

1. When at a dead-end it backtracks through the path until it reaches a cell with unvisited neighbours, continuing from there. 

1. until every cell has been visited, the computer would backtrack all the way to the beginning cell. 

1. Entire maze space is guaranted a complete visit.

### side note

> To add difficulty and a fun factor to the DFS, you can __influence the likelihood of which neighbor you should visit__, instead of completely random. 

> By making it more likely to visit neighbors to your sides, you can have a more horizontal maze generation.  
