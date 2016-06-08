---
layout: post
title: "[CC150v4] 20.11 Find Subsquare with Black Border "
comments: true
category: CC150v4

---

### Question

> Imagine you have a square matrix, where each cell is filled with either black or white. 

> Design an algorithm to find the maximum subsquare such that all four borders are filled with black pixels. 

### Solution

There is no better way to solve this except Brute Force. First find a point (as the top-left corner), and then test square size from large to small. 

The code below is from the book. 

### Code

	public static Subsquare findMaxSquareInMatrix(int[][] matrix) {
		assert (matrix.length > 0);
		for (int row = 0; row < matrix.length; row++) {
			assert (matrix[row].length == matrix.length);
		}

		int N = matrix.length;
		int currentMaxSize = 0;
		Subsquare sq = null;
		int col = 0;

		// Iterate through each column from left to right
		while (N - col > currentMaxSize) { // See step 4 above
			for (int row = 0; row < matrix.length; row++) {
				// starting from the biggest
				int size = N - Math.max(row, col);
				while (size > currentMaxSize) {
					if (checkSquareBorders(matrix, row, col, size)) {
						currentMaxSize = size;
						sq = new Subsquare(row, col, size);
						break; // go to next (full) column
					}
					size--;
				}
			}
			col++;
		}
		return sq;
	}

	private static boolean checkSquareBorders(int[][] matrix, int row, int col,
			int size) {
		// Check top and bottom border.
		for (int j = 0; j < size; j++) {
			if (matrix[row][col + j] == 1) {
				return false;
			}
			if (matrix[row + size - 1][col + j] == 1) {
				return false;
			}
		}

		// Check left and right border.
		for (int i = 1; i < size - 1; i++) {
			if (matrix[row + i][col] == 1) {
				return false;
			}
			if (matrix[row + i][col + size - 1] == 1) {
				return false;
			}
		}
		return true;
	}
