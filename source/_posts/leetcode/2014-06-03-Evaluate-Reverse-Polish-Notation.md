---
layout: post
title: "[LeetCode 150] Evaluate Reverse Polish Notation"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/evaluate-reverse-polish-notation/)

<div class="question-content bg-color bg-img font-color">
            <p class="font-color"></p><p class="font-color">
Evaluate the value of an arithmetic expression in <a href="http://en.wikipedia.org/wiki/Reverse_Polish_notation" class="font-color">Reverse Polish Notation</a>.
</p>

<p class="font-color">
Valid operators are <code>+</code>, <code>-</code>, <code>*</code>, <code>/</code>. Each operand may be an integer or another expression.
</p>

<p class="font-color">
Some examples:<br>
</p><pre>  ["2", "1", "+", "3", "*"] -&gt; ((2 + 1) * 3) -&gt; 9
  ["4", "13", "5", "/", "+"] -&gt; (4 + (13 / 5)) -&gt; 6
</pre>
<p class="font-color"></p><p class="font-color"></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a classic question__. It's easy.

### Code

__my code__

    public int evalRPN(String[] tokens) {
        if (tokens == null || tokens.length == 0)
        	return 0;
        Stack<Integer> stack = new Stack<Integer>();
        for (int p = 0; p < tokens.length; p ++) {
        	char cur = tokens[p].charAt(0);
        	if (cur >= '0' && cur <= '9' 
        			|| tokens[p].length() > 1)
        		stack.push(Integer.parseInt(tokens[p]));
        	else if (cur == '+') {
        		int num1 = stack.pop();
        		int num2 = stack.pop();
        		stack.push(num1 + num2);
        	}
        	else if (cur == '-') {
        		int num1 = stack.pop();
        		int num2 = stack.pop();
        		stack.push(num2 - num1);
        	}
        	else if (cur == '*') {
        		int num1 = stack.pop();
        		int num2 = stack.pop();
        		stack.push(num1 * num2);
        	}
        	else if (cur == '/') {
        		int num1 = stack.pop();
        		int num2 = stack.pop();
        		stack.push(num2 / num1);
        	}
        }
        return stack.pop();
    }
