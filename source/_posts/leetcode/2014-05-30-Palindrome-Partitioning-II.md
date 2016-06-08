---
layout: post
title: "[LeetCode 132] Palindrome Partitioning II"
comments: true
category: Leetcode

---

### Question 
[link](https://oj.leetcode.com/problems/palindrome-partitioning-ii/)

<div class="question-content">
            <p></p><p>
Given a string <i>s</i>, partition <i>s</i> such that every substring of the partition is a palindrome.
</p>
<p>
Return the minimum cuts needed for a palindrome partitioning of <i>s</i>.
</p>
<p>
For example, given <i>s</i> = <code>"aab"</code>,<br>
Return <code>1</code> since the palindrome partitioning <code>["aa","b"]</code> could be produced using 1 cut.
</p><p></p>
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
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is DP, but not traditional DP question__

#### IT IS DOUBLE DP! 

It is very hard for me to even understand the solution, but __I have found a great analysis from [peking2's blog](http://blog.sina.com.cn/s/blog_b9285de20101iwqt.html)__. 

> 这题一般人一看就是DP，DP公式也很容易推出，算是一道简单的DP。

> dp(i) = min( 1+dp(j+1), if substring(i,j) is palindrome)

> 从以上的分析时间复杂度为O(n^3), 主要是因为检查回文也需要O(n)的时间。因此这题有意思的一点就是如何降低时间复杂度到O(n^2)？

> __其实这题是两个DP混杂在了一起__，这也是这道题最有意思的地方。另外一个DP就是跟检查回文有关了，公式如下

> dp(i)(j)=true if s(i)==s(j) && dp(i+1)(j-1)

> 也就是说，你要检查一个回文只需要知道头尾的字符相等，并且中间的字串已经成为了回文即可。O(1)复杂度。

__A more detailed analysis is available in [this blog](http://fisherlei.blogspot.sg/2013/03/leetcode-palindrome-partitioning-ii.html)__. 

<blockquote cite="http://fisherlei.blogspot.sg/2013/03/leetcode-palindrome-partitioning-ii.html">

    <b>[Thoughts]</b>
    <br>凡是求最优解的，一般都是走DP的路线。这一题也不例外。首先求dp函数，
    <br>
    <br>定义函数
    <br>D[i,n] = 区间[i,n]之间最小的cut数，n为字符串长度
    <br>
    <br>&nbsp;a &nbsp; b &nbsp; a &nbsp; b &nbsp; b &nbsp; b &nbsp; a &nbsp; b &nbsp; b &nbsp; a &nbsp; b &nbsp; a
    <br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;i &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;n
    <br>如果现在求[i,n]之间的最优解？应该是多少？简单看一看，至少有下面一个解
    <br>
    <br>
    <br>&nbsp;a &nbsp; b &nbsp; a &nbsp; b &nbsp; b &nbsp; b &nbsp; a &nbsp; b &nbsp; b &nbsp; a &nbsp; b &nbsp; a
    <br>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;i &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;
    <span style="color: red;">j</span>&nbsp;
    <span style="color: red;">j+1</span>&nbsp; &nbsp; n
    <br>
    <br>此时 &nbsp;D[i,n] = min(D[i, j] + D[j+1,n]) &nbsp;i&lt;=j &lt;n。这是个二维的函数，实际写代码时维护比较麻烦。所以要转换成一维DP。如果每次，从i往右扫描，每找到一个回文就算一次DP的话，就可以转换为
    <br>D[i] = 区间[i,n]之间最小的cut数，n为字符串长度， 则,
    <br>
    <br>D[i] = min(1+D[j+1] ) &nbsp; &nbsp;i&lt;=j &lt;n
    <br>
    <br>有个转移函数之后，一个问题出现了，就是如何判断[i,j]是否是回文？每次都从i到j比较一遍？太浪费了，这里也是一个DP问题。
    <br>定义函数
    <br>P[i][j] = true if [i,j]为回文
    <br>
    <br>那么
    <br>P[i][j] = str[i] == str[j] &amp;&amp; P[i+1][j-1];
    <br>
</blockquote>

### Solution

The coding is not easy, especially __when 2 DP are written in 1 for-loop__. 

I wrote many times until I finally achieved the nice and concise solution that you see below. 

### Code

__Doing everything in 1 loop__, not an intuitive code. 

    public int minCut(String s) {
        int len = s.length();
        if (len <= 1) return 0;
        boolean[][] pl = new boolean[len][len];
        int[] dp = new int[len];
        for (int i = len-1; i >= 0; i --) {
            dp[i] = Integer.MAX_VALUE;
            for (int j = i; j < len; j ++) {
                // first set pl[][], then update dp[i]
                if (j - i <= 1) pl[i][j] = s.charAt(i) == s.charAt(j);
                else pl[i][j] = s.charAt(i) == s.charAt(j) & pl[i+1][j-1];
                if (pl[i][j]) {
                    if (j == len-1) dp[i] = 0;
                    else 
                        dp[i] = Math.min(dp[i], dp[j+1] + 1);
                }
            }
        }
        return dp[0];
    }

__Updated on July 18th, 2014__, written by me. 

    boolean[][] map = null;
    
    public int minCut(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }
        map = getMap(s);
        int len = s.length();
        int[] dp = new int[len + 1];
        dp[0] = -1;
        for (int i = 0; i < len; i++) {
            dp[i+1] = Integer.MAX_VALUE;
            for (int j = 0; j <= i; j++) {
                if (map[j][i]) {
                    dp[i+1] = Math.min(dp[i+1], dp[j] + 1);
                }
            }
        }
        return dp[len];
    }
	
	private boolean[][] getMap(String s) {
		int len = s.length();
		boolean[][] map = new boolean[len][len];
		for (int i = len - 1; i >= 0; i--) {
			for (int j = 0; j < len; j++) {
				if (i > j) {
				    continue;
				} else if (i == j) {
				    map[i][j] = true;
				} else {
				    if (i + 1 == j) {
				        map[i][j] = s.charAt(i) == s.charAt(j);
				    } else {
				        map[i][j] = s.charAt(i) == s.charAt(j) && map[i+1][j-1];
				    }
				}
			}
		}
		return map;
	}
