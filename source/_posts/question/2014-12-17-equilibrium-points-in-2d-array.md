---
layout: post
title: "[Question] Equilibrium Points in 2D Array "
comments: true
category: Question

---

### Question

[link](http://get-that-job-at-google.blogspot.sg/2013/01/twitter-programming-test.html)

> In a 2D matrix of dimensions M*N, find number of "equilibrium" points.  A point (i, j) is said to be an "equilibrium" point only if all following conditions hold:

> a) sum of rows 1...(i-1) =  sum of rows (i+1)...M

> b) sum of columns 1...(j-1)  = sum of columns (j+1)...N

### Solution

This is a generalize question of __Equilibrium index__.

Refer to __Equilibrium index__, read [this](http://www.geeksforgeeks.org/equilibrium-index-of-an-array/). __The idea__ is to get total sum of array first. Then Iterate through the array calculate left sum == sum / 2. 

> Equilibrium index of an array is an index such that the sum of elements at lower indexes is equal to the sum of elements at higher indexes. For example, in an arrya A:

> A[0] = -7, A[1] = 1, A[2] = 5, A[3] = 2, A[4] = -4, A[5] = 3, A[6]=0

> 3 is an equilibrium index, because:
A[0] + A[1] + A[2] = A[4] + A[5] + A[6]

> 6 is also an equilibrium index, because sum of zero elements is zero, i.e., A[0] + A[1] + A[2] + A[3] + A[4] + A[5]=0

Well, for Equilibrium Points in 2D Array, should be similar. DIY and leave me a comment! 

### Code

__code for [findning EI in 1-D array](http://rosettacode.org/wiki/Equilibrium_index#Java)__

	public List<Integer> findEI(int[] array) {
		List<Integer> ans = new ArrayList<Integer>();
		int sum = 0;
		for (int i = 0; i < array.length; i++) {
			sum += array[i];
		}
		int runningSum = 0;
		for (int i = 0; i < array.length; i++) {
			if (2 * runningSum + array[i] == sum) {
				ans.add(i);
			}
			runningSum += array[i];
		}
		return ans;
	}
