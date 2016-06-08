---
layout: post
title: "[LeetCode 53] Maximum Subarray"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/maximum-subarray/)

<div class="question-content">
            <p></p><p>
Find the contiguous subarray within an array (containing at least one number) which has the largest sum.
</p>
<p>
For example, given the array <code>[−2,1,−3,4,−1,2,1,−5,4]</code>,<br>
the contiguous subarray <code>[4,−1,2,1]</code> has the largest sum = <code>6</code>.
</p>

<div class="spoilers"><b>More practice:</b>

<p>If you have figured out the O(<i>n</i>) solution, try coding another solution using the divide and conquer approach, which is more subtle.</p>
</div><p></p>
</div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
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

__This problem can be solved using DP or Divide and Conquer__.

DP solution is very easy. I will only post the code. 

__Divide and Conquer approach is difficult__. Not only the idea of solution is hard to come up with, the coding part is even more challenging, __especially when the input array contains all negative numbers__! 

### Solution

First 2 code posted below are DP solutions. 

__2nd code is from [this article](http://cs.slu.edu/~goldwasser/courses/slu/csci314/2012_Fall/lectures/maxsubarray/) (Algorithm 3)__. The idea is to divide the list by half, and find the max of this 3 values: 

1. max subarray to the left of mid-point (exclusive)
2. max subarray to the right of mid-point (exclusive)
3. max subarray from left of mid-point to the right of mid-point (inclusive)

For 1 and 2 are easy, for 3 is not. It needs to read left until the end, and right until the end (which means basically read n times). __The total time complexity is O(nlgn)__. 

__3rd code is from [this blog](http://fisherlei.blogspot.sg/2012/12/leetcode-maximum-subarray.html)__. It's exactly same method, just coding a bit different. 

Note there can be negative number! We can not initiate sum to 0. Instead I should do Integer.MIN_VALUE. Meanwhile, the sum should be initiated to 0, and cannot be Integer.MIN_VALUE. 

### My code

	public class Solution {
	    public int maxSubArray(int[] A) {
	        if (A == null || A.length == 0) {
	            return 0;
	        }
	        int pre = 0;
	        int max = Integer.MIN_VALUE;
	        for (int i = 0; i < A.length; i++) {
	            max = Math.max(max, pre + A[i]);
	            pre = Math.max(0, pre + A[i]);
	        }
	        return max;
	    }
	}

__2nd code__

    public int maxSubArray(int[] A) {
        return recmax(A, 0, A.length - 1);
    }

    private int recmax(int[] A, int l, int u) {
        if (l > u) /* zero elements */
            return 0;
        if (l == u) /* one element */
            return Math.max(Integer.MIN_VALUE, A[l]);
        int m = (l + u) / 2;
        /* find max crossing to left */
        int lmax = Integer.MIN_VALUE;
        int sum = 0;
        for (int i = m; i >= l; i--) {
            sum += A[i];
            lmax = Math.max(lmax, sum);
        }
        int rmax = Integer.MIN_VALUE;
        sum = 0;
        /* find max crossing to right */
        for (int i = m + 1; i <= u; i++) {
            sum += A[i];
            rmax = Math.max(rmax, sum);
        }
        return Math.max(Math.max(recmax(A, l, m), recmax(A, m + 1, u)), lmax
                + rmax);
    }

__3rd code__

    public int maxSubArray(int[] A) {
        return maxArray(A, 0, A.length - 1, Integer.MIN_VALUE);
    }

    private int maxArray(int A[], int left, int right, int maxV) {
        if (left > right) return Integer.MIN_VALUE;
        int mid = (left + right) / 2;
        int lmax = maxArray(A, left, mid - 1, maxV);
        int rmax = maxArray(A, mid + 1, right, maxV);
        maxV = Math.max(Math.max(maxV, lmax), rmax);
        int sum = 0, mlmax = 0;
        for (int i = mid - 1; i >= left; i--) {
            sum += A[i];
            if (sum > mlmax) mlmax = sum;
        }
        sum = 0;
        int mrmax = 0;
        for (int i = mid + 1; i <= right; i++) {
            sum += A[i];
            if (sum > mrmax) mrmax = sum;
        }
        maxV = Math.max(maxV, mlmax + mrmax + A[mid]);
        return maxV;
    }
