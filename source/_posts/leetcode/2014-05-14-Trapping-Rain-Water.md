---
layout: post
title: "[LeetCode 42] Trapping Rain Water "
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/trapping-rain-water/)

<div class="question-content">
            <p></p><p>
Given <i>n</i> non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining. 
</p>

<p>
For example, <br>
Given <code>[0,1,0,2,1,0,1,3,2,1,2,1]</code>, return <code>6</code>.
</p>

<p>
<img src="http://www.leetcode.com/wp-content/uploads/2012/08/rainwatertrap.png"><br>
</p><p style="font-size: 11px">The above elevation map is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped. <b>Thanks Marcos</b> for contributing this image!</p><p></p>
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

__This is an interesting question__. 

__Most popular solution is DP__. The explanation from [this blog](http://rleetcode.blogspot.sg/2014/03/trapping-rain-water-java-python.html) is slightly confusing, so I will explain it here. __Basic idea is to do 2 iteration__. First time get the heighest bound to the left of every point. Second time get the heighest bound to the right. 

> Example: input = \[0,1,0,2,1,0,1,3,2,1,2,1\]. 

> Assume the 2 DP arrays are called highestLeftSoFar and highestRightSoFar.

> highestLeftSoFar  = 0,1,1,2,2,2,2,3,3,3,3,3

> highestRightSoFar = 3,3,3,3,3,3,3,3,2,2,2,1

> For each point, get the lowest bound (of the 2 bounds), and calculate water. 

__There is another solution__ making use of stack from [this blog](http://n00tc0d3r.blogspot.sg/2013/06/trapping-rain-water.html). This idea is IMHO not very good.

{% img middle /assets/images/trapping_rain.png %}

1. Use Stack to store the index of a bar;
2. If the current one is smaller then the top of the stack, push it to stack;
3. Otherwise, pop up the top until stack is empty or top is greater than the current one, add up the volume, push the current one to stack.

> The tricky part is what is the volume to be added each time when we pop up a value from the stack.

### My code 

    public class Solution {
        public int trap(int[] A) {
            if (A == null || A.length <= 1) {
                return 0;
            }
            int len = A.length;
            int[] leftBound = new int[len];
            for (int i = 1; i < len; i++) {
                leftBound[i] = Math.max(leftBound[i - 1], A[i - 1]);
            }
            int rightBound = 0;
            int water = 0;
            for (int i = len - 2; i > 0; i--) {
                rightBound = Math.max(rightBound, A[i + 1]);
                int contains = Math.min(leftBound[i], rightBound);
                // important to note, that contains can be 0!
                water += Math.max(0, contains - A[i]);
            }
            return water;
        }
    }

Stack Solution.

    public int trap(int[] A) {
        int cur = 0;
        while (cur < A.length && A[cur] == 0) cur ++;
        int vol = 0;
        Stack<Integer> stack = new Stack<Integer>();
        while (cur < A.length) {
            while (!stack.isEmpty() && A[cur] >= A[stack.peek()]) {
                int b = stack.pop();
                if (stack.isEmpty()) break;
                vol += ((cur - stack.peek() - 1) * (Math.min(A[cur], A[stack.peek()]) - A[b]));
            }
            stack.push(cur ++);
            cur ++;
        }
        return vol;
    }

__updated on Aug 27th, 2014__, there is a very very good 2 pointer solution which reads the input only __once__! 

[This post](http://qandwhat.runkite.com/i-failed-a-twitter-interview/) wrote about it, and [source code](https://gist.github.com/mkozakov/59af0fd5bddbed1a0399) available. 

    public int trap(int[] A) {
        if (A == null || A.length == 0) {
			return 0;
		}
		
		int len = A.length;
		int left = 0;
		int right = len - 1;
		int leftHeight = 0;
		int rightHeight = 0;
		int water = 0;
		
		while (left < right) {
			leftHeight = Math.max(leftHeight, A[left]);
			rightHeight = Math.max(rightHeight, A[right]);
			// Two ways to write the following if-condition 
			// This would also work: if (A[left] < A[right]) {
			if (leftHeight < rightHeight) {
				// increase left pointer
				water += leftHeight - A[left];
				left++;
			} else {
				water += rightHeight - A[right];
				right--;
			}
		}
		return water;
    }
