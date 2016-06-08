---
layout: post
title: "[LeetCode 96] Unique Binary Search Trees"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/unique-binary-search-trees/)

<div class="question-content">
            <p></p><p>Given <i>n</i>, how many structurally unique <b>BST's</b> (binary search trees) that store values 1...<i>n</i>?</p>

<p>
For example,<br>
Given <i>n</i> = 3, there are a total of 5 unique BST's.

</p><pre>   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
</pre>
<p></p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="white">1</td>
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
		<td bgcolor="lime">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This seems like an easy recursion question__, however it will result in many repeated recursion calls. 

To avoid repeated recursion, use __Dynamic Programming__. 

### Solution

First code below is my solution. It is __a standard recursion solution__, but it's not good. The run time is 30ms more than next code. 

Second code is __DP solution__, where the previous answers are saved and used forfuture calculation. This is the best solution for this question, and I learnt it from [this blog](https://github.com/shengmin/coding-problem/blob/master/leetcode/unique-binary-search-trees/Solution.java). 

### Code

__First code__

    public int numTrees(int n) {
        if (n <= 1) return 1;
        
        int total = 0;
        if (n % 2 == 0){
            for (int i = 0; i <= n / 2 - 1; i ++ ){
                // i is all the possible number of nodes on the left
                total += 2 * numTrees(i) * numTrees(n-i-1);
            }
        } else {
            for (int i = 0; i <= (n-1) / 2 - 1; i ++ ){
                // i is all the possible number of nodes on the left
                total += 2 * numTrees(i) * numTrees(n-i-1);
            }
            total += Math.pow(numTrees((n-1)/2), 2);
        }
        return total;
    }

__Second code__

    public int numTrees(int n) {
        int[] table = new int[n + 1];
        table[0] = 1;
        table[1] = 1;
        for (int i = 2; i <= n; i++) {
            int sum = 0;
            for (int j = 1; j <= i; j++) {
                int left = j - 1;
                int right = i - j;
                sum += table[left] * table[right];
            }
            table[i] = sum;
        }
        return table[n];
    }
