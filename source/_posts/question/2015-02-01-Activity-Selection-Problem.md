---
layout: post
title: "[Greedy] Activity Selection Problem "
comments: true
category: Question

---

[link](http://www.geeksforgeeks.org/greedy-algorithms-set-1-activity-selection-problem/)

### Question 

> Given n activities with their start and finish times. 

> Select maximum number of activities that can be performed in one run. 

> Example:

         start[]  =  {1, 3, 0, 5, 8, 5};
         finish[] =  {2, 4, 6, 7, 9, 9};

         output[] = {0, 1, 3, 4}

### Solution

__Greedy algorithm__, according to [gfg](http://www.geeksforgeeks.org/greedy-algorithms-set-1-activity-selection-problem/): 

1. Sort the activities according to their finishing time

1. Select the first activity from the sorted array and print it.

1. For the rest, if start time is greater than previous finish time, then select this activity.

### Code

not written.
