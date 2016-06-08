---
layout: post
title: "[LeetCode 130] Surrounded Regions"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/surrounded-regions/)

<div class="question-content">
            <p></p><p>
Given a 2D board containing <code>'X'</code> and <code>'O'</code>, capture all regions surrounded by <code>'X'</code>.</p>

<p>A region is captured by flipping all <code>'O'</code>s into <code>'X'</code>s in that surrounded region.
</p>

<p>
For example,<br>
</p><pre>X X X X
X O O X
X X O X
X O X X
</pre>
<p></p>

<p>
After running your function, the board should be:
</p><pre>X X X X
X X X X
X X X X
X O X X
</pre>
<p></p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This question can be solved by DFS or BFS search__. 

__The idea is simple__. For each edge nodes, if it is an 'O', search for all connected 'O's and mark it. My first attemps used another array to store result. It works, but it's actually bad, because space usage is huge. We can actually mark the connected nodes using some special character, for example in my case, 'R'. Then the solution can work in-place. 

So this is the standard solution. 

### Solution

However, there is __one big problem__ with my DFS solution. 

__For super-large test cases, it gets 'java.lang.StackOverflowError' exception__. It's very werid to me, until I read [this blog](https://oj.leetcode.com/discuss/1723/my-code-can-not-pass-this-longest-case). 

> If you use DFS Recursive, you will get Runtime Error. But if you implement DFS by stack, just like doing BFS by Queue, your code will get accepted. 

> Recursive dfs would take too much resource (too many calls which require space to store the calling state) than bfs for long long case. Considering one of test case with 200x200 matrix, in worst case the longest path (number of calls) might take 200x200 = 40,000 long. While with bfs, the maximal calls are about less than 400. 

One more thing, so __DFS with stack, or BFS with queue, which one would consume less space__? I think BFS. The difference is DFS space usage is max depth, while BFS is the max width. However in this question, each node have 4 adjacent nodes, so the DFS space usage would be increased to 3 x (max depth). More details on this topic, please refer to __DFS, BFS and space efficiency__. 

If any reader have an idea on this, please comment!

### Code

__bfs code realized with a queue__

    public void solve(char[][] board) {
        if (board.length == 0) return;
        int m = board.length, n = board[0].length;
        for (int i = 0; i < m; i ++) {
            dfs(board, i, 0);
            dfs(board, i, n-1);
        }
        for (int j = 0; j < n; j ++) {
            dfs(board, 0, j);
            dfs(board, m-1, j);
        }
		for (int i = 0; i < m; i ++) 
			for (int j = 0; j < n; j ++) 
				if (board[i][j] == 'R') 
					board[i][j] = 'O';
				else if (board[i][j] == 'O') 
					board[i][j] = 'X';
    }
    
    private void dfs(char[][] board, int x, int y) {
        int m = board.length, n = board[0].length;
        Queue<Integer> aa = new LinkedList<Integer>();
        Queue<Integer> bb = new LinkedList<Integer>();
        aa.add(x);
        bb.add(y);
        while (!aa.isEmpty()) {
            int a = aa.remove();
            int b = bb.remove();
			if (a < 0 || a >= m || b < 0 || b >= n) 
				continue;
            if (board[a][b] == 'X' || board[a][b] == 'R') 
				continue;
            board[a][b] = 'R';
			
			aa.add(a - 1);
			bb.add(b);
			aa.add(a + 1);
			bb.add(b);
			aa.add(a);
			bb.add(b - 1);
			aa.add(a);
			bb.add(b + 1);
        }
    }

