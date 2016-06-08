---
layout: post
title: "[Question] Find row with most 1s "
comments: true
category: Question

---

### Question

[link](http://www.geeksforgeeks.org/find-the-row-with-maximum-number-1s/)

> Given a 2D array with only 1s and 0s, where each row is sorted. 

> Find the row with the maximum number of 1s. Input matrix: 

    0 1 1 1
    0 0 1 1
    1 1 1 1  // this row has maximum 1s
    0 0 0 0

> Output: 2

### Analysis

By using a modified version of binary search, we can achieve __[a O(mLogn) solution](http://www.geeksforgeeks.org/find-the-row-with-maximum-number-1s/)__ where m is number of rows and n is number of columns in matrix. 

__However, there's better solution that works in linear time__! 

### Solution 

1. Get the index of first (or leftmost) 1 in the first row. 

2. Do following for every row after the first row: 

    1. IF the element on left of previous leftmost 1 is 0, ignore this row. 
    
    1. ELSE Move left until a 0 is found. Update the leftmost index to this index and max_row_index to be the current row. 

The time complexity is O(m+n). 

### Code 

__written by me__

	public int solution(int[][] matrix) {
		int m = matrix.length;
		int n = matrix[0].length;
		int p = n;
		int row = -1;
		for (int i = 0; i < m; i++) {
			// now p is larger than 0, otherwise it's already terminated
			if (matrix[i][p - 1] == 0) {
				continue;
			}
			// p points to a 1, now search to the left direction
			for (int j = p - 1; j >= 0; j--) {
				if (matrix[i][j] == 1) {
					p = j;
				} else {
					break;
				}
			}
			// p have a new value now
			if (p == 0) {
				return i;
			} else {
				row = i;
			}
		}
		return row;
	}
