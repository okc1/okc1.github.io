---
layout: post
title: "[LeetCode 4] Median of Two Sorted Arrays "
comments: true
category: Leetcode

---

### Question 

[link](https://oj.leetcode.com/problems/median-of-two-sorted-arrays/)

<div class="question-content">
    <p></p>
    
    <p>There are two sorted arrays A and B of size m and n respectively. Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).
    </p>
    
    <p></p>
</div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
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

__This is a tough question__. 

__If the size of the 2 arrays (i.e. m and n) are same__, this would become a much easier question with simple "Divide and Conquer" solution. Well, not extremely easy like everyone can solve it, but a much simpler one. I do recommend you to read more at [this post](http://www.geeksforgeeks.org/median-of-two-sorted-arrays/) before you procceed. 

However, this question is not as simple. Let's talk about it. 

### Solution

__This first solution is well covered in the [MIT CLRS handouts](http://www2.myoops.org/course_material/mit/NR/rdonlyres/Electrical-Engineering-and-Computer-Science/6-046JFall-2005/30C68118-E436-4FE3-8C79-6BAFBB07D935/0/ps9sol.pdf)__. The basic idea is, finding the median of the first array, then assuming this number is the final median, and look where this element should have been put in the second array. There are 3 possible conditions. For example, if the arrays are {1, 4, 5, 6, 26} and {2, 13, 34}. We first get number 5, and compare it with 13. Then we know that median shall be large than 5, and we continue this (like) binary search with O(lgn) complexity. This solution is complex and difficult in thinking. I would like to focus on a different solution. 

__Second solution, credit goes to [ninechap](http://answer.ninechapter.com/solutions/median-of-two-sorted-arrays/)__. Finding the median is like finding the (k)th element from the combination of 2 arrays. We might have to search for (k)th element twice, but the overall complexity is always O(lg n). 

### My code 

    public class Solution {
        public double findMedianSortedArrays(int A[], int B[]) {
            if (A == null || B == null) {
                return 0;
            }
            int len = A.length + B.length;
            int mid1 = (len + 1) / 2;
            int mid2 = len / 2 + 1;
            // there are chances the mid1 == mid2, (i.e. when odd elements) 
            // for simplicity of the code, leave it this way. I admit I'm lazy. 
            return ((double) getKth(A, B, 0, 0, mid1) 
                    + getKth(A, B, 0, 0, mid2)) / 2;
        }

        private int getKth(int A[], int B[], int start1, int start2, int k) {
            // note that k start from 1, not from 0
            int len1 = A.length;
            int len2 = B.length;
            if (start1 >= len1) {
                // all elements in A is used up.
                return B[start2 + k - 1];
            } else if (start2 >= len2) {
                return A[start1 + k - 1];
            }
            // now both A and B have elements left
            if (k == 1) {
                return Math.min(A[start1], B[start2]);
            } else {
                // eliminate half of k. Since k >=2: 
                int half = k / 2;
                int mid1 = start1 + half - 1;
                int mid2 = start2 + half - 1;
                // this is the critical part. We now have mid1 and mid2
                // and we try to eliminate all element to the left of
                // either mid1 or mid2 (inclusively)
                // so what I need is to compare the value of A[mid1] and B[mid2]
                int val1 = Integer.MAX_VALUE;
                if (mid1 < len1) {
                    val1 = A[mid1];
                }
                int val2 = Integer.MAX_VALUE;
                if (mid2 < len2) {
                    val2 = B[mid2];
                }
                // this is another important point. mid1 and mid2 may be out of bound
                // if so, the value should be MAX_VALUE because median could not fall on the other array
                // why? draw it yourself and you'll see. I can't explain without a picture. 
                if (val1 > val2) {
                    // discard mid2 and all elements to the left of it. 
                    return getKth(A, B, start1, mid2 + 1, k - half);
                } else {
                    return getKth(A, B, mid1 + 1, start2, k - half);
                }
            }
        }
    }

Note: starting from today, I would post my code with more focus on __readability__, instead of conciseness. Sometimes, the former is much more important than the latter. 
