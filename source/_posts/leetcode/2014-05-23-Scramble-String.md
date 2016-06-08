---
layout: post
title: "[LeetCode 87] Scramble String"
comments: true
category: Leetcode

---

### Question 
[link](https://oj.leetcode.com/problems/scramble-string/)

<div class="question-content">
            <p></p><p>
Given a string <i>s1</i>, we may represent it as a binary tree by partitioning it to two non-empty substrings recursively.
</p>
<p>
Below is one possible representation of <i>s1</i> = <code>"great"</code>:
</p>
<pre>    great
   /    \
  gr    eat
 / \    /  \
g   r  e   at
           / \
          a   t
</pre>
<p>
To scramble the string, we may choose any non-leaf node and swap its two children.
</p>
<p>
For example, if we choose the node <code>"gr"</code> and swap its two children, it produces a scrambled string <code>"rgeat"</code>.
</p>
<pre>    rgeat
   /    \
  rg    eat
 / \    /  \
r   g  e   at
           / \
          a   t
</pre>
<p>
We say that <code>"rgeat"</code> is a scrambled string of <code>"great"</code>.
</p>
<p>
Similarly, if we continue to swap the children of nodes <code>"eat"</code> and <code>"at"</code>, it produces a scrambled string <code>"rgtae"</code>.
</p>
<pre>    rgtae
   /    \
  rg    tae
 / \    /  \
r   g  ta  e
       / \
      t   a
</pre>
<p>
We say that <code>"rgtae"</code> is a scrambled string of <code>"great"</code>.
</p>
<p>
Given two strings <i>s1</i> and <i>s2</i> of the same length, determine if <i>s2</i> is a scrambled string of <i>s1</i>.
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
		<td bgcolor="red">5</td>
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

This is problem can be solved by __either DFS or DP.__

__[This blog](http://zhaohongze.com/wordpress/2013/12/12/leetcode-scramble-string/) have a very good analysis of the DFS approach__. 

<blockquote>
<p>Note that the binary tree can be constructed arbitrarily. So the general idea to tackle this problem is to enumerate every possible binary trees using DFS to see if two strings are scrambled strings. We can accelerate this process by adding a very efficient pruning.<br>
Given two strings, s1, s2. First check if they have same letters and same length, denote as len.<br>
For any l (1 &lt;= l &lt;= len): partition s1 into s11 = s1[0 : l), s12 = s1[l : len). We have two ways to partition s1:</p>
<ol>
<li>s21 = s2[0 : 1), s22 = s2[l : len). In this case, check s11 and s21 have same letters and are scrambled strings. And check s12 and s22 have same letters and are scrambled strings</li>
<li>s21 = s2[0 : len – l), s22 = s2[len – l : len). In this case, check s11 and s22 have same letters and are scrambled strings. Then check s12 and s21 have same letters and are scrambled strings </li>
</ol>
</blockquote>
    
__[This blog](http://blog.sina.com.cn/s/blog_b9285de20101gy6n.html) have a very good DP analysis__.

<blockquote>
<span style="font-family: Arial; vertical-align: baseline; white-space: pre-wrap;">
dp[i][j][k] 代表了s1从i开始，s2从j开始，长度为k的两个substring是否为scramble
string。</span><br>
<span style="font-family: Arial; vertical-align: baseline; white-space: pre-wrap;">
有三种情况需要考虑：</span><br>
<span style="font-family: Arial; vertical-align: baseline; white-space: pre-wrap;">
1. 如果两个substring相等的话，则为true</span><br>
<span style="font-family: Arial; vertical-align: baseline; white-space: pre-wrap;">
2. 如果两个substring中间某一个点，左边的substrings为scramble string，
同时右边的substrings也为scramble string，则为true</span><br>
<span style="font-family: Arial; vertical-align: baseline; white-space: pre-wrap;">
3. 如果两个substring中间某一个点，s1左边的substring和s2右边的substring为scramble
string, 同时s1右边substring和s2左边的substring也为scramble
string，则为true</span><br>
</blockquote>

For more explanation, [this blog](http://yihuad.blogspot.sg/2013/10/scramble-string-leetcode.html) and [this blog](http://www.blogjava.net/sandy/archive/2013/05/22/399605.html) and [this blog](http://blog.csdn.net/linhuanmars/article/details/24506703) have discussed about it. 

### Code

__my code__

    public boolean isScramble(String s1, String s2) {
        if (! sameLetters(s1, s2)) return false;
        if (s1.equals(s2)) return true;
        for (int i = 1; i < s1.length(); i ++) {
            String left1 = s1.substring(0,  i);
            String right1 = s1.substring(i, s1.length());
            String left2 = s2.substring(0,  i);
            String right2 = s2.substring(i, s2.length());
            if (isScramble(left1, left2) && isScramble(right1, right2))
                return true;
            left2 = s2.substring(0, s2.length() - i);
            right2 = s2.substring(s2.length() - i, s2.length());
            if (isScramble(left1, right2) && isScramble(right1, left2))
                return true;
        }
        return false;
    }

    private boolean sameLetters(String a, String b) {
        if (a.length() != b.length()) return false;
        int[] count = new int[26];
        for (Character aa: a.toCharArray()) 
            count[aa - 'a'] ++;
        for (Character bb: b.toCharArray()) 
            if (count[bb - 'a'] -- <= 0) 
                return false;
        return true;
    }

__Updated on July 5th, 2014__: written again with less substring operations and more variables inside the method: 

    public boolean isScramble(String s1, String s2) {
        if (s1 == null || s2 == null || s1.length() != s2.length()) {
            return false;
        }
        int len = s1.length();
        return helper(s1, 0, len - 1, s2, 0, len - 1);
    }
    
    private boolean helper(String s1, int a1, int b1, String s2, int a2, int b2) {
        if (a1 - b1 != a2 - b2) 
            return false;
        // check s1[a1, b1] and s2[a2, b2] have same set of letters
        int[] count = new int[26];
        for (int i = a1; i <= b1; i++) 
            count[s1.charAt(i) - 'a'] ++;
        for (int i = a2; i <= b2; i++) 
            if (count[s2.charAt(i) - 'a'] -- <= 0) 
                return false;
        // check s1[a1, b1] and s2[a2, b2] is scramble or not
        if (a1 == b1) {
            return (s1.charAt(a1) == s2.charAt(a2));
        }
        for (int i = 0; i < b1 - a1; i++) {
            boolean check = helper(s1, a1, a1 + i, s2, a2, a2 + i) 
                        && helper(s1, a1 + i + 1, b1, s2, a2 + i + 1, b2);
            if (check) return true;
            check = helper(s1, a1, a1 + i, s2, b2 - i, b2) 
                        && helper(s1, a1 + i + 1, b1, s2, a2, b2 - i - 1);
            if (check) return true;
        }
        return false;
    }

__DP code__, not written by me 

    public boolean isScramble(String s1, String s2) {
        int n = s1.length();
        boolean[][][] dp = new boolean[n][n][n + 1];
        for (int i = n - 1; i >= 0; i--)
            for (int j = n - 1; j >= 0; j--)
                for (int k = 1; k <= n - Math.max(i, j); k++) {
                    if (s1.substring(i, i + k).equals(s2.substring(j, j + k)))
                        dp[i][j][k] = true;
                    else {
                        for (int l = 1; l < k; l++) {
                            if (dp[i][j][l] && dp[i + l][j + l][k - l] 
                                || dp[i][j + k - l][l] && dp[i + l][j][k - l]) {
                                dp[i][j][k] = true;
                                break;
                            }
                        }
                    }
                }
        return dp[0][0][n];
    }
