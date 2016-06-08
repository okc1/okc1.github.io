---
layout: post
title: "[LeetCode 71] Simplify Path"
comments: true
category: Leetcode

---

### Question 
[link](https://oj.leetcode.com/problems/simplify-path/)

<div class="question-content">
            <p></p><p>Given an absolute path for a file (Unix-style), simplify it.</p>

<p>For example,<br>
<b>path</b> = <code>"/home/"</code>, =&gt; <code>"/home"</code><br>
<b>path</b> = <code>"/a/./b/../../c/"</code>, =&gt; <code>"/c"</code><br>
</p>

<div class="spoilers" ><b>Corner Cases:</b>

<p>
</p><ul>
<li>Did you consider the case where <b>path</b> = <code>"/../"</code>?<br>
In this case, you should return <code>"/"</code>.</li>
<li>Another corner case is the path might contain multiple slashes <code>'/'</code> together, such as <code>"/home//foo/"</code>.<br>
In this case, you should ignore redundant slashes and return <code>"/home/foo"</code>.</li>
<p></p>
</ul></div><p></p>
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
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a very difficult string question__. I read [this blog](http://fisherlei.blogspot.sg/2013/01/leetcode-simplify-path.html) and then understands the question. The solution is just straight-forward without any fancy algo/thinkings. 

<blockquote cite="http://fisherlei.blogspot.sg/2013/01/leetcode-simplify-path.html">
    <br>
    [解题思路]<br>
    利用栈的特性，如果sub string element<br>
    1. 等于“/”，跳过，直接开始寻找下一个element<br>
    2. 等于“.”，什么都不需要干，直接开始寻找下一个element<br>
    3. 等于“..”，弹出栈顶元素，寻找下一个element<br>
    4. 等于其他，插入当前elemnt为新的栈顶，寻找下一个element<br>
    <br>
    最后，再根据栈的内容，重新拼path。这样可以避免处理连续多个“/”的问题。<br>
    <br>
</blockquote>

### Solution

Simply make use of stack and read thru all substrings seperated by /. 

### Code


    public String simplifyPath(String path) {
        Stack<String> stack = new Stack<String>();
        String[] list = path.split("/");
        for(String cur: list) {
            if (cur.equals("/") || cur.equals(".")
                || cur.equals("")) continue;
            if (cur.equals("..")) {
                if (! stack.isEmpty()) stack.pop();
            } else stack.push(cur);
        }
        String ans = "";
        if (stack.isEmpty()) return "/";
        while (! stack.isEmpty()) {
            ans = "/" + stack.pop() + ans;
        }
        return ans;
    }
