---
layout: post
title: "[LeetCode 174] Dungeon Game "
comments: true
category: Leetcode
---

### Question

[link](https://leetcode.com/problems/dungeon-game/)

<div class="question-content">
              <p><style>
table.dungeon, .dungeon th, .dungeon td {
  border:3px solid black;
}

 .dungeon th, .dungeon td {
    text-align: center;
    height: 70px;
    width: 70px;
}
</style>

</p><p>The demons had captured the princess (<b>P</b>) and imprisoned her in the bottom-right corner of a dungeon. The dungeon consists of M x N rooms laid out in a 2D grid. Our valiant knight (<b>K</b>) was initially positioned in the top-left room and must fight his way through the dungeon to rescue the princess. </p>
<p>The knight has an initial health point represented by a positive integer. If at any point his health point drops to 0 or below, he dies immediately. </p>
<p>Some of the rooms are guarded by demons, so the knight loses health (<i>negative</i> integers) upon entering these rooms;
other rooms are either empty (<i>0's</i>) or contain magic orbs that increase the knight's health (<i>positive</i> integers).</p>
<p>In order to reach the princess as quickly as possible, the knight decides to move only rightward or downward in each step. </p>

<br>
<p><b>Write a function to determine the knight's minimum initial health so that he is able to rescue the princess.</b></p>
<p>For example, given the dungeon below, the initial health of the knight must be at least <b>7</b> if he follows the optimal path <code>RIGHT-&gt; RIGHT -&gt; DOWN -&gt; DOWN</code>.</p>

<table class="dungeon">
<tbody><tr>
<td>-2 (K)</td>
<td>-3</td>
<td>3</td>
</tr>
<tr>
<td>-5</td>
<td>-10</td>
<td>1</td>
</tr>
<tr>
<td>10</td>
<td>30</td>
<td>-5 (P)</td>
</tr>
</tbody></table>
<!---2K   -3  3
-5   -10   1
10 30   5P-->

<br>
<p><b>Notes:</b>
</p><ul>
<li>The knight's health has no upper bound.</li>
<li>Any room can contain threats or power-ups, even the first room the knight enters and the bottom-right room where the princess is imprisoned.  </li>
</ul>
<p></p>

<p><b>Credits:</b><br>Special thanks to <a href="https://oj.leetcode.com/discuss/user/stellari">@stellari</a> for adding this problem and creating all test cases.</p><p></p>

                <div id="tags" class="btn btn-xs btn-warning">Show Tags</div>
                <span class="hide">

                  <a class="btn btn-xs btn-primary" href="/tag/dynamic-programming/">Dynamic Programming</a>

                  <a class="btn btn-xs btn-primary" href="/tag/binary-search/">Binary Search</a>

                </span>

            </div>

### Analysis

The key of solving this problem is to __do DP from bottom right to top left__.

### Solution

dp[i][j] means the minimum initial value of each position. As suggested by[](http://www.cnblogs.com/grandyang/p/4233035.html), the DP equation is:

> dp[i][j] = max(1, min(dp[i+1][j], dp[i][j+1]) - dungeon[i][j]).

### Code

    public class Solution {
        public int calculateMinimumHP(int[][] dungeon) {
            if (dungeon == null) return 1;
            int m = dungeon.length;
            int n = dungeon[0].length;

            int[][] dp = new int[m][n];
            for (int i = m - 1; i >= 0; i--) {
                for (int j = n - 1; j >= 0; j--) {
                    if (i == m - 1 && j == n - 1) {
                        dp[i][j] = Math.max(1, 1 - dungeon[i][j]);
                    } else if (i == m - 1) {
                        dp[i][j] = Math.max(1, dp[i][j + 1] - dungeon[i][j]);
                    } else if (j == n - 1) {
                        dp[i][j] = Math.max(1, dp[i + 1][j] - dungeon[i][j]);
                    } else {
                        dp[i][j] = Math.max(1,
                            Math.min(dp[i + 1][j], dp[i][j + 1]) - dungeon[i][j]);
                    }
                }
            }
            return dp[0][0];
        }
    }
