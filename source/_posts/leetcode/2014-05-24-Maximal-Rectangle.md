---
layout: post
title: "[LeetCode 85] Maximal Rectangle"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/maximal-rectangle/)

<div class="question-content">
            <p></p><p>
Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing all ones and return its area.
</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="white">1</td>
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

__This is a very difficult question__. It is similar and also related to "__Largest Rectangle in Histogram__". 

Two solutions are available for this question. 

__First solution is O(n^2)__. This makes use of solution of "__Largest Rectangle in Histogram__", which is to say, we are finding the max rectangle for each row (as base) in the matrix. 

This solution is very easy to write once you realize this connection - I guess not many people would. That's why I have the next solution. 

__Second solution is a clever Brute Force, time complexity is O(n^3)__. The fundamental idea is to make a 2-D array storing the number of '1's occured before current node (inclusive). After this is done, there're 2 different ways to implement. Read code 2 and code 3. 

### Solution

FIrst code is easy. 

Second code is the idea from [this blog](http://blog.csdn.net/fightforyourdream/article/details/17711893). For every node in the 2-D array, checks all possible rectangles ending at this node (which mean check all the way up/left). 

Third code from [this blog](http://leetcodenotes.wordpress.com/2013/10/19/leetcode-maximal-rectangle-0101%E7%BB%84%E6%88%90%E7%9A%84%E7%9F%A9%E9%98%B5%EF%BC%8C%E6%B1%82%E9%87%8C%E9%9D%A2%E5%85%A8%E6%98%AF1%E7%9A%84%E7%9F%A9%E5%BD%A2%E7%9A%84%E6%9C%80%E5%A4%A7%E9%9D%A2/). It is similar to second, but it's checking all rectangles that shared same width as current line. So it's checking up then down, both direction. Read the code and it's easy to understand. 

### Code

__First, solution making use of "Largest rectangle"__

    public int maximalRectangle(char[][] matrix) {
        if (matrix.length == 0 || matrix[0].length == 0) return 0;
        int[][] m = new int[matrix.length][matrix[0].length];
        for (int i = 0; i < matrix.length; i ++) {
            for (int j = 0; j < matrix[i].length; j ++) {
                if (i == 0 || matrix[i][j] == '0') 
                    m[i][j] = matrix[i][j] - '0';
                else 
                    m[i][j] = m[i-1][j] + 1;
            }
        }
        int max = 0;
        for (int i = 0; i < m.length; i ++) {
            max = Math.max(max, largestRectangleArea(m[i]));
        }
        return max;
    }

    // the following code is the solution for "Largest Rectangle in Histogram"
    public int largestRectangleArea(int[] height) {
        int len = height.length;
        if (len == 0) return 0;
        int max = Integer.MIN_VALUE;
        Stack<Integer> stack = new Stack<Integer>();
        for (int i = 0; i < len; i ++) {
            if (stack.isEmpty() || height[stack.peek()] <= height[i]) stack.push(i);
            else {
                int temp = stack.pop();
                // here I must do a check of stack.isEmpty(), 
                // And do nto use (i-height[temp]) instead use (i-stack.peek()-1])
                max = Math.max(max, height[temp] * 
                    (stack.isEmpty() ? i : (i - stack.peek() - 1)));
                i --;
            }
        }
        while (! stack.isEmpty()) {
                int temp = stack.pop();
                max = Math.max(max, height[temp] * 
                    (stack.isEmpty() ? len : (len - stack.peek() - 1)));
        }
        return max;
    }

__Second __

    public int maximalRectangle(char[][] matrix) {
        int rows = matrix.length;  
        if (rows == 0) return 0;  
        int cols = matrix[0].length;  
        int [][] hOnes = new int[rows][cols];
        int max = 0;
        for (int i=0; i<rows; i++)
            for(int j=0; j<cols; j++) 
                if(matrix[i][j] == '1')
                    if(j == 0) hOnes[i][j] = 1;
                    else hOnes[i][j] = hOnes[i][j-1] + 1;
        for (int i=0; i<rows; i++)
            for (int j=0; j<cols; j++){  
                if (hOnes[i][j] != 0){  
                    int minI = i;
                    int minRowWidth = hOnes[i][j];
                    while (minI >= 0){
                        minRowWidth = Math.min(minRowWidth, hOnes[minI][j]);  
                        int area = minRowWidth * (i-minI+1);  
                        max = Math.max(max, area);  
                        minI--;  
                    }
                }
            }
        return max;  
    }

__Third__

    public int maximalRectangle(char[][] matrix) {
        if (matrix.length == 0) return 0;
        int res = 0;
        int m = matrix.length, n = matrix[0].length;
        int[][] d = new int[m][n];
        for (int i = 0; i < m; i++) {
            d[i][0] = matrix[i][0] - '0';
            for (int j = 1; j < n; j++) 
                d[i][j] = matrix[i][j] == '1' ? d[i][j - 1] + 1 : 0;
        }
        for (int i = 0; i < m; i++) 
            for (int j = 0; j < n; j++) 
                res = Math.max(res, expand(d, i, j));
        return res;
    }
    
    private int expand(int[][] d, int I, int J) {
        int height = 0, width = d[I][J];
        //go up
        for (int i = I - 1; i >= 0; i--)
            if (d[i][J] >= width) height++;
            else break;
        //go down
        for (int i = I; i < d.length; i++) 
            if (d[i][J] >= width) height++;
            else break;
        return width * height;
    }
