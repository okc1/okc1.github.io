---
layout: post
title: "[LeetCode 200] Number of Islands "
comments: true
category: Leetcode
---

### Question 

[link](https://leetcode.com/problems/number-of-islands/)

<div class="question-content">
              <p></p><p>Given a 2d grid map of <code>'1'</code>s (land) and <code>'0'</code>s (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.</p>

<p><i><b>Example 1:</b></i></p>
<pre>11110<br>11010<br>11000<br>00000</pre>
<p>Answer: 1</p>
<p><i><b>Example 2:</b></i></p>
<pre>11000<br>11000<br>00100<br>00011</pre>
<p>Answer: 3</p>

<p><b>Credits:</b><br>Special thanks to <a href="https://leetcode.com/discuss/user/mithmatt">@mithmatt</a> for adding this problem and creating all test cases.</p><p></p>
              
                <div id="tags" class="btn btn-xs btn-warning">Show Tags</div>
                <span class="hide">
                  
                  <a class="btn btn-xs btn-primary" href="/tag/depth-first-search/">Depth-first Search</a>
                  
                  <a class="btn btn-xs btn-primary" href="/tag/breadth-first-search/">Breadth-first Search</a>
                  
                </span>
              
            </div>

### Analysis

At every '1' position, do DFS.

### Solution

I post my code below. Note that we do not actually have to have the method "findLand" -  we can simply read through the grid and mark all '1's in one run. 

You might want to come up with your own code. Mine is just for reference. This is not an very interesting question, I assume. 

### Code

    public class Solution {
        public int numIslands(char[][] grid) {
            if (grid == null || grid.length == 0 || grid[0].length == 0) {
                return 0;
            }
            int m = grid.length;
            int n = grid[0].length;
            int count = 0;

            Pair firstPiece = findLand(grid, m, n);
            while (firstPiece != null) {
                // mark all neighbors, and count increment
                mark(grid, m, n, firstPiece);
                firstPiece = findLand(grid, m, n);
                count++;
            }

            return count;
        }

        void mark(char[][] grid, int m, int n, Pair p) {
            if (p.x < 0 || p.x == m || p.y < 0 || p.y == n) {
                return;
            } else if (grid[p.x][p.y] != '1') {
                return;
            }
            // mark current and then dfs
            grid[p.x][p.y] = '2';
            mark(grid, m, n, new Pair(p.x - 1, p.y));
            mark(grid, m, n, new Pair(p.x + 1, p.y));
            mark(grid, m, n, new Pair(p.x, p.y - 1));
            mark(grid, m, n, new Pair(p.x, p.y + 1));
        }

        Pair findLand(char[][] grid, int m, int n) {
            for (int i = 0; i < m; i++) {
                for (int j = 0; j < n; j++) {
                    if (grid[i][j] == '1') {
                        return new Pair(i, j);
                    }
                }
            }
            return null;
        }

        class Pair {
            int x;
            int y;

            public Pair(int a, int b) {
                x = a;
                y = b;
            }
        }
    }

