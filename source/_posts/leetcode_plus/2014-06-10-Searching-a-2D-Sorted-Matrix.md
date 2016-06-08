---
layout: post
title: "[LeetCode Plus] Searching a 2D Sorted Matrix"
comments: true
category: leetcode_plus
tags: [ unit test needed ]
---


### Question 

[link](http://leetcode.com/2010/10/searching-2d-sorted-matrix.html)

<blockquote>
<p class="font-color">Write an efficient algorithm that searches for a value in an <i>n</i> x <i>m</i> table (two-dimensional array). This table is sorted along the rows and columns — that is,</p><p class="font-color">Table[i][j] ≤ Table[i][j + 1], <br>Table[i][j] ≤ Table[i + 1][j]</p>
</blockquote>

### Related questions

__[Search a 2D Matrix]({% post_url /leetcode/2014-05-21-Search-a-2D-Matrix %})__. 

__[Searching a 2D Sorted Matrix]({% post_url /leetcode_plus/2014-06-10-Searching-a-2D-Sorted-Matrix %})__. 

__[Count negative in a 2D Sorted Matrix]({% post_url /question/2014-06-14-Count-negative-in-2D-Sorted-Matrix %})__. 

### Analysis 

This is a extremely high-freq question. Almost every company will ask. 

This question is not to be confused with __[Search a 2D Matrix]({% post_url /leetcode/2014-05-21-Search-a-2D-Matrix %})__. 

__Solution One: Step-wise Linear Search__. Standard solution. 

Time = O(n). Worse case 2n steps.

Note that __this is the best solution__! 

{% img middle /assets/images/search_2D_matrix_1.png %}

> begin with the upper right corner, we traverse one step to the left or bottom. For example, the picture below shows the traversed path (the red line) when we search for 13.
    Essentially, each step we are able to eliminate either a row or a column.

__Solution Two: Quad Partition 四分法__. 

Time = O(n^1.58). Analysis can be found in the original question post. 

{% img middle /assets/images/search_2D_matrix_2.png %}

Basic idea is like binary search - get mid and divide. We can then discard 1/4 of the matrix. For example: search for 6, we can discard the bottom right sub-matrix. 

__Solution Three: Diagonal-based binary partition__. This is based on previous solution, but better. 

Time = O(nlgn). 

{% img middle /assets/images/search_2D_matrix_3.png %}

This is a good solution, but it would fail in a non-square matrix, so...

### Code

__step-wise linear search__

    bool stepWise(int mat[][N_MAX], int N, int target, 
                  int &row, int &col) {
      if (target < mat[0][0] || target > mat[N-1][N-1]) return false;
      row = 0;
      col = N-1;
      while (row <= N-1 && col >= 0) {
        if (mat[row][col] < target) 
          row++;
        else if (mat[row][col] > target)
          col--;
        else
          return true;
      }
      return false;
    }
