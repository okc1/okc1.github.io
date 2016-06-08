---
layout: post
title: "[LeetCode 79] Word Search"
comments: true
categories:
- Leetcode
- z-string-search

---


### Question 
[link](https://oj.leetcode.com/problems/word-search/)

<div class="question-content">
            <p></p><p>
Given a 2D board and a word, find if the word exists in the grid.
</p>
<p>
The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.
</p>

<p>
For example,<br>
Given <b>board</b> = 
</p><pre>[
  ["ABCE"],
  ["SFCS"],
  ["ADEE"]
]
</pre>

<b>word</b> = <code>"ABCCED"</code>, -&gt; returns <code>true</code>,<br>
<b>word</b> = <code>"SEE"</code>, -&gt; returns <code>true</code>,<br>
<b>word</b> = <code>"ABCB"</code>, -&gt; returns <code>false</code>.<br>
<p></p><p></p>
</div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Solution

__This is a very classical DFS question__. Writing this solution fast and precise is very importnt. 

The solution is recursive DFS search. 

__The second code posted below comes from [this blog](http://needjobasap.blogspot.sg/2014/01/word-search-leetcode.html)__. The code is slightly shorter because it checks __visited_array__ at the beginning of search() method, instead of for each directions. Other than that, it's basically same solution. 

### Code

__First, my code__


    public boolean exist(char[][] board, String word) {
        if (word.length() == 0) return true;
        int m = board.length, n = board[0].length;
        for (int i = 0; i < m; i ++) {
            for (int j = 0; j < n; j ++) {
                if (board[i][j] == word.charAt(0)) {
                    int[][] visited = new int[m][n];
                    visited[i][j] = 1;
                    boolean ans = find(i, j, board, visited, word.substring(1));
                    if (ans) return true;
                }
            }
        }
        return false;
    }

    private boolean find(int a, int b, char[][] board, int[][] visited, 
                        String word) {
        if (word.length() == 0) return true;
        int m = board.length, n = board[0].length;
        char target = word.charAt(0);
        if (a > 0 && visited[a-1][b] == 0 && board[a-1][b] == target) {
            visited[a - 1][b] = 1;
            boolean ans = find(a - 1, b, board, visited, word.substring(1));
            if (ans) return true;
            visited[a - 1][b] = 0;
        } // top
        if (a < m - 1 && visited[a+1][b] == 0 && board[a+1][b] == target) {
            visited[a + 1][b] = 1;
            boolean ans = find(a + 1, b, board, visited, word.substring(1));
            if (ans) return true;
            visited[a + 1][b] = 0;
        } // bottom
        if (b > 0 && visited[a][b-1] == 0 && board[a][b-1] == target) {
            visited[a][b - 1] = 1;
            boolean ans = find(a, b - 1, board, visited, word.substring(1));
            if (ans) return true;
            visited[a][b - 1] = 0;
        } // left
        if (b < n - 1 && visited[a][b+1] == 0 && board[a][b+1] == target) {
            visited[a][b + 1] = 1;
            boolean ans = find(a, b + 1, board, visited, word.substring(1));
            if (ans) return true;
            visited[a][b + 1] = 0;
        } // right
        return false;
    }


__Second, code from blog__


    public boolean exist(char[][] board, String word) {
        int height = board.length;
        int width = board[0].length;
        boolean[][] visited = new boolean[height][width];
        for (int i = 0; i < height; i++) 
            for (int j = 0; j < width; j++) 
                if (search(board, visited, i, j, word, 0)) 
                    return true;
        return false;
    }

    private boolean search(char[][] board, boolean[][] visited, 
            int row, int col, String word, int index) {
        if (word.charAt(index) != board[row][col]) 
            return false;
        if (index == word.length() - 1) 
            return true;

        int height = board.length;
        int width = board[0].length;
        visited[row][col] = true;
        //up
        if (row > 0 && !visited[row - 1][col] 
                && search(board, visited, row - 1, col, word, index + 1)) 
            return true;
        //down
        if (row < height - 1 && !visited[row + 1][col] 
                && search(board, visited, row + 1, col, word, index + 1)) 
            return true;
        //left
        if (col > 0 && !visited[row][col - 1] 
                && search(board, visited, row, col - 1, word, index + 1)) 
            return true;
        //right
        if (col < width - 1 && !visited[row][col + 1] 
                && search(board, visited, row, col + 1, word, index + 1)) 
            return true;
        // if we did not find the path we need set this position as unvisited
        visited[row][col] = false;

        return false;
    }
