---
layout: post
title: "[LeetCode 84] Largest Rectangle in Histogram"
comments: true
category: Leetcode

---

### Question 
[link](https://oj.leetcode.com/problems/largest-rectangle-in-histogram/)

<div class="question-content">
            <p></p><p>
Given <i>n</i> non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.
</p>

<p>
<img src="http://www.leetcode.com/wp-content/uploads/2012/04/histogram.png"><br>
</p><p style="font-size: 11px">Above is a histogram where width of each bar is 1, given height = <code>[2,1,5,6,2,3]</code>.</p>
<p></p>

<p>
<img src="http://www.leetcode.com/wp-content/uploads/2012/04/histogram_area.png"><br>
</p><p style="font-size: 11px">The largest rectangle is shown in the shaded area, which has area = <code>10</code> unit.</p>
<p></p>

<p>
For example,<br>
Given height = <code>[2,1,5,6,2,3]</code>,<br>
return <code>10</code>.
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
		<td bgcolor="red">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is an extremely difficult question__. 

The idea of the solution (using stack) seems understandable, but can be very tricky when coding. 

__The basic idea is, always keep increasing elements in the stack__. When I see a decrease in number, pop stack. And I calculate max area only when poping elements. In the end, a '0' is inserted to the end, so that all stack item will be popped (and at the same time, max area been calculated). 

Sorry if I did not explain well enough. [Here](http://www.geeksforgeeks.org/largest-rectangle-under-histogram/) is a better one: 

<blockquote cite="http://www.geeksforgeeks.org/largest-rectangle-under-histogram/">
<p>
We traverse all bars from left to right, maintain a stack of bars.  Every bar is pushed to stack once.  A bar is popped from stack when a bar of smaller height is seen.  When a bar is popped, we calculate the area with the popped bar as smallest bar. How do we get left and right indexes of the popped bar – the current index tells us the ‘right index’ and index of previous item in stack is the ‘left index’.  Following is the complete algorithm.
</p>
<p><strong>1) </strong>Create an empty stack.</p>
<p><strong>2) </strong>Start from first bar, and do following for every bar ‘hist[i]‘ where ‘i’ varies from 0 to n-1.<br>
……<strong>a)</strong> If stack is empty or hist[i] is higher than the bar at top of stack, then push ‘i’ to stack.<br>
……<strong>b)</strong> If this bar is smaller than the top of stack, then keep removing the top of stack while top of the stack is greater. Let the removed bar be hist[tp]. Calculate area  of rectangle with hist[tp] as smallest bar. For hist[tp], the ‘left index’ is previous (previous to tp) item in stack and ‘right index’ is ‘i’ (current index).</p>
<p><strong>3)</strong> If the stack is not empty, then one by one remove all bars from stack and do step 2.b for every removed bar.</p>
</blockquote>

Time complexity of the stack solution is __O(n)__. (Another algo analysis article [here](http://tech-queries.blogspot.sg/2011/03/maximum-area-rectangle-in-histogram.html)) 

### Solution

__I wrote the code using idea from [blog](http://jane4532.blogspot.sg/2013/07/longest-rectangle-in-histogramleetcode.html)__. It works, but there are 2 things that I got wrong. 

__First, if elements are equal__. I shall also push it. I can not simply skip it, I don't know why! 

> if (stack.isEmpty() || cur >= height[stack.peek()]) 

__Second, about how to calculate the width of the rectangle__. I used this before: 

> int width = stack.isEmpty() ? p : p - h;

It's wrong, I must get the value of next element from stack, and then calculate width. Why? there might be element been popped before, which locate between these 2 elements in stack. 

> int width = stack.isEmpty() ? p : p - stack.peek() - 1;

__Updated on July 4th, 2014__: the above 2 points are very valid, especially the second. Keep in mind: 

1. The values in stack means the last position that a height can be found. For example, height is (2, 10, 5) then the stack would have (2, removed, 5). When calculating the area for height 5, we should note the removed space is in consideration as well. 

1. So, when equal height is found, pop it. Because you won't need it any more. The stack only stores last position this height is found.

1. When stack is empty, the width of rectange should be calculated from 0. 

### Code

__My code written on July 4th, 2014__

    public int largestRectangleArea(int[] height) {
        if (height == null || height.length == 0) {
            return 0;
        }
        Stack<Integer> stack = new Stack<Integer>();
        stack.add(0);
        int len = height.length;
        int area = 0;
        for (int i = 1; i <= len; i++) {
            int h = i == len ? 0 : height[i];
            // pop a element and calculate its max area
            // pop until the top element is smaller than h, then push h
            while (!stack.isEmpty() && h <= height[stack.peek()]) {
                int pos = stack.pop();
                int width = stack.isEmpty() ? i : i - stack.peek() - 1;
                area = Math.max(area, height[pos] * width);
            }
            stack.push(i);
        }
        return area;
    }

__My code written on July 18th, 2014__

    public int largestRectangleArea(int[] height) {
        if (height == null || height.length == 0) {
			return 0;
		}
		int maxArea = Integer.MIN_VALUE;
		Stack<Integer> stack = new Stack<Integer>();
		int p = 0;
		while (p < height.length) {
			if (stack.isEmpty() || height[stack.peek()] <= height[p]) {
				stack.push(p);
				p++;
			} else {
				int h = stack.pop();
			    int w = stack.isEmpty() ? p : p - stack.peek() - 1;
				int area = height[h] * w;
				maxArea = Math.max(maxArea, area);
			}
		}
		while (!stack.isEmpty()) {
			int h = stack.pop();
			int w = stack.isEmpty() ? p : p - stack.peek() -1;
			int area = height[h] * w;
			maxArea = Math.max(maxArea, area);
		}
		return maxArea;
    }
