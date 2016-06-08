---
layout: post
title: "[LeetCode 131] Palindrome Partitioning"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/palindrome-partitioning/)

<div class="question-content">
            <p></p><p>
Given a string <i>s</i>, partition <i>s</i> such that every substring of the partition is a palindrome.
</p>
<p>
Return all possible palindrome partitioning of <i>s</i>.
</p>
<p>
For example, given <i>s</i> = <code>"aab"</code>,<br>

Return
</p><pre>  [
    ["aa","b"],
    ["a","a","b"]
  ]
</pre>
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
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is an extremely classic question__. 

It's not very hard to solve, although it looked impossible at first. 

### Solution

__The solution is DFS__. 

It's very standard DFS code, I will not go into coding details. This type of "return all possible path" question is always related to DFS, keep this in mind! 

The code is borrowing ideas from [peking2's blog](http://blog.sina.com.cn/s/blog_b9285de20101jbtl.html). He also had an __analysis on this series of questions__: 

> 我觉得一般有三种变形，解法各有不同。

> 1. 最后结果是一个整数，比如Palindrome Partitioning II。这个用DP来解
> 2. 最后求一个结果，比如最小切法。这个用DP＋backtrack来解
> 3. 求所有的结果。这个一般用DFS来解。

This question is the 3rd case. [Fish Lei](http://fisherlei.blogspot.sg/2013/03/leetcode-palindrome-partitioning.html) also said the same. 

> 这种需要输出所有结果的基本上都是DFS的解法

### Code

    public ArrayList<ArrayList<String>> partition(String s) {
        // int len = s.length();
        ArrayList<ArrayList<String>> ans = new ArrayList<ArrayList<String>>();
        helper(ans, new ArrayList<String>(), s, 0);
        return ans;
	}
	
	private void helper(ArrayList<ArrayList<String>> ans, ArrayList<String> cur, 
	        String s, int start) {
	    int len = s.length();
	    if (start == len) {
	        ans.add(new ArrayList<String>(cur));
	        return;
	    }
	    for (int i = start + 1; i <= len; i ++) {
	        String sub = s.substring(start, i);
	        if (isPal(sub)) {
	            cur.add(sub);
	            helper(ans, cur, s, i);
	            cur.remove(cur.size() - 1);
	        }
	    }
	}
	
	private boolean isPal(String str) {
    	int left = 0, right = str.length() - 1;
    	while (left < right) {
    		if (str.charAt(left) != str.charAt(right)) 
    			return false;
    		left++;
    		right--;
    	}
    	return true;
	}
