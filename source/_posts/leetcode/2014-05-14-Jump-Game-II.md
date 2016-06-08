---
layout: post
title: "[LeetCode 45] Jump Game II "
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/jump-game-ii/)

<div class="question-content">
<p></p><p>
Given an array of non-negative integers, you are initially positioned at the first index of the array.
</p>
<p>
Each element in the array represents your maximum jump length at that position. 
</p>
<p>
Your goal is to reach the last index in the minimum number of jumps.
</p>

<p>
For example:<br>
Given array A = <code>[2,3,1,1,4]</code>
</p>
<p>
The minimum number of jumps to reach the last index is <code>2</code>. (Jump <code>1</code> step from index 0 to 1, then <code>3</code> steps to the last index.)
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
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Solution

__This is a DP problem__. But we do not have to save all values into a DP array. 

__A analysis of DP solution__ from [this blog](http://eric-yuan.me/leetcode-jump-game-ii/) explains it very well: 

> Search forward, and see for each node of array, what is the current maximum place we can reach, and every time we reach a local maximum, we add counter by 1, if we can reach the terminal, just return the counter.

It's easy to get "time limit exceed" if you solve this problem like a traditional DP question. 

So __I come up with a solution using 2 pointers__: 'left' and 'right' that denotes the boundary that can be jumps to within a certain number of jumps. What I need to do is updating the 2 pointers and increase the counter for number of jumps. 

### My code 

traditional DP

    public class Solution {
        public int jump(int[] A) {
            int len = A.length;
            if (len <= 1) return 0;
            int[] dp = new int[len];
            if (A[0] == 0) return 0;
            int cur = 1;
            for (int i = 0; i < len; i ++) {
                if (i != 0 && dp[i] == 0) 
                    return 0;
                // array dp represent the steps to reach point i
                for (; cur < len && cur <= i + A[i]; cur ++) {
                    dp[cur] = dp[i] + 1;
                }
                if (dp[len - 1] != 0) 
                    return dp[len - 1];
            }
            return 0;
        }
    }

DP without array (recommended)

	public class Solution {
	    public int jump(int[] A) {
	        if (A == null || A.length <= 1) {
	            return 0;
	        }
	        int len = A.length;
	        // note that this is a DP question, but considering the required out, 
	        // we do not need dp array (i.e.) 
	        // int[] dp = new int[len];
	        
	        int jumps = 0;
	        int left = 0;
	        int right = 0;
	        
	        while (right < len) {
	            int reachable = right;
	            jumps++;
	            for (int i = left; i <= right; i++) {
	                reachable = Math.max(reachable, i + A[i]);
	            }
	            if (reachable == right) {
	                // unable to jump forward
	                return -1;
	            }
	            if (reachable >= len - 1) {
	                return jumps;
	            } else {
	                left = right + 1;
	                right = reachable;
	            }
	        }
	        return -1;
	    }
	}

non-DP

    public class Solution {
        public int jump(int[] A) {
            if (A == null || A.length <= 1) {
                return 0;
            }
            int len = A.length;
            // note that this is a DP question, but considering the required out, 
            // we do not need dp array (i.e.) 
            // int[] dp = new int[len];

            int jumps = 0;
            int left = 0;
            int right = 0;

            while (right < len) {
                int reachable = right;
                jumps++;
                for (int i = left; i <= right; i++) {
                    reachable = Math.max(reachable, i + A[i]);
                }
                if (reachable == right) {
                    // unable to jump forward
                    return -1;
                }
                if (reachable >= len - 1) {
                    return jumps;
                } else {
                    left = right + 1;
                    right = reachable;
                }
            }
            return -1;
        }
    }
