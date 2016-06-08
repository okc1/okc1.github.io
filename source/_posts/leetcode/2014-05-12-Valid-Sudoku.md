---
layout: post
title: "[LeetCode 36] Valid Sudoku"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/valid-sudoku/)

<div class="question-content">
            <p></p><p>Determine if a Sudoku is valid, according to: <a href="http://sudoku.com.au/TheRules.aspx">Sudoku Puzzles - The Rules</a>.</p>

<p>The Sudoku board could be partially filled, where empty cells are filled with the character <code>'.'</code>.</p>

<p>
<img src="http://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png"><br>
</p><p style="font-size: 11px">A partially filled sudoku which is valid.</p>
<p></p>

<p><b>Note:</b><br>
A valid Sudoku board (partially filled) is not necessarily solvable. Only the filled cells need to be validated.
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
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Solution

__This is not a difficult problem__. 

Make use of __three for-loops__ and __nine arrays of length 9__ (for each loop) to mark the status, then do DFS search. 

However, __I also found a very concise solution__. Read below. 

### My code 

    public class Solution {
        public boolean isValidSudoku(char[][] board) {
            if (board == null || board.length == 0) {
                return false;
            }
            int N = board.length;
            for (int i = 0; i < N; i++) {
                boolean[] foo = new boolean[N];
                // validate each row
                for (int j = 0; j < N; j++) {
                    if (board[i][j] != '.') {
                        if (foo[board[i][j] - '1']) {
                            return false;
                        }
                        foo[board[i][j] - '1'] = true;
                    }
                }
                foo = new boolean[N];
                // validate each column
                for (int j = 0; j < N; j++) {
                    if (board[j][i] != '.') {
                        if (foo[board[j][i] - '1']) {
                            return false;
                        }
                        foo[board[j][i] - '1'] = true;
                    }
                }
            }
            for (int a = 0; a < 3; a++) {
                for (int b = 0; b < 3; b++) {
                    boolean[] foo = new boolean[N];
                    for (int c = 0; c < 3; c++) {
                        for (int d = 0; d < 3; d++) {
                            if (board[a * 3 + c][b * 3 + d] != '.') {
                                if (foo[board[a * 3 + c][b * 3 + d] - '1']) {
                                    return false;
                                }
                                foo[board[a * 3 + c][b * 3 + d] - '1'] = true;
                            }
                        }
                    }
                }
            }
            return true;
        }
    }

__The following solution__ is from [this blog](http://www.cnblogs.com/zhaolizhen/p/Sudoku.html). It's a very clever and surprisingly concise code. 

    public boolean isValidSudoku(char[][] board) {
        boolean[][] rows = new boolean[9][9];
        boolean[][] cols = new boolean[9][9];
        boolean[][] blocks = new boolean[9][9];
        for (int i = 0; i < 9; ++i) {
            for (int j = 0; j < 9; ++j) {
                int c = board[i][j] - '1';
                if (board[i][j] == '.') continue;
                if (rows[i][c] || cols[j][c] || blocks[i - i % 3 + j / 3][c])
                    return false;
                rows[i][c] = cols[j][c] = blocks[i - i % 3 + j / 3][c] = true;
            }
        }
        return true;
    }
