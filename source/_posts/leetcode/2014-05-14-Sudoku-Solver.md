---
layout: post
title: "[LeetCode 37] Sudoku Solver"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/sudoku-solver/)

<div class="question-content">
<p></p><p>Write a program to solve a Sudoku puzzle by filling the empty cells.</p>

<p>Empty cells are indicated by the character <code>'.'</code>.</p>

<p>You may assume that there will be only one unique solution.

</p><p>
<img src="http://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png"><br>
</p><p style="font-size: 11px">A sudoku puzzle...</p>
<p></p>

<p>
<img src="http://upload.wikimedia.org/wikipedia/commons/thumb/3/31/Sudoku-by-L2G-20050714_solution.svg/250px-Sudoku-by-L2G-20050714_solution.svg.png"><br>
</p><p style="font-size: 11px">...and its solution numbers marked in red.
</p><p></p>
          </div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Solution

__This is a very classic DFS search problem__, and it is not easy.

The solution simply brute force DFS. Read more at [this blog](http://xixiaogualu.blogspot.sg/2013/09/leetcode-sudoku-solver.html).

### My code 

    public class Solution {
        public void solveSudoku(char[][] board) {
            if (board == null || board.length == 0) {
                return;
            }
            int N = board.length;
            board = helper(board, N, 0, 0);
        }

        private char[][] helper(char[][] board, int N, int x, int y) {
            if (x == N) {
                return board;
            } else if (y == N) {
                return helper(board, N, x + 1, 0);
            } else if (board[x][y] != '.') {
                // made a mistake here with (y+1) instead of (x+1) 
                return helper(board, N, x, y + 1);
            } else {
                // put in from 1 to 9, and then check validation
                for (int i = 1; i <= 9; i++) {
                    board[x][y] = (char) ('0' + i);
                    if (isValid(board, x, y)) {
                        // if the number we just put in is valid inside the board
                        char[][] ans = helper(board, N, x, y + 1);
                        if (ans != null) {
                            return ans;
                        } else {
                            // putting in this number (i) will not work, so...
                            // put in next number and try, until 9
                        }
                    }
                    // this is important for backtarcking - set the char back to its original value!!! 
                    board[x][y] = '.';
                }
            }
            // in fact, we can just return true/false for this question. 
            return null;
        }

        // this validation method we borrowed from my old code
        private boolean isValid(char[][] board, int i, int j) {
            boolean[] map = new boolean[9];
            for (int k = 0; k < 9; k++) 
                if (k != j && board[i][k] == board[i][j])
                    return false;
            for (int k = 0; k < 9; k++) 
                if (k != i && board[k][j] == board[i][j])
                    return false;
            for (int row = i / 3 * 3; row < i / 3 * 3 + 3; row++) 
                for (int col = j / 3 * 3; col < j / 3 * 3 + 3; col++) 
                    if ((row != i || col != j) && board[row][col] == board[i][j])
                        return false;
            return true;
        }
    }
