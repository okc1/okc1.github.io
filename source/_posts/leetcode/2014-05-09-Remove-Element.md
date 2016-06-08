---
layout: post
title: "[LeetCode 27] Remove Element"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/remove-element/)

<div class="question-content">
            <p></p><p>Given an array and a value, remove all instances of that value in place and return the new length.
</p>

<p>
The order of elements can be changed. It doesn't matter what you leave beyond the new length.
</p><p></p>
</div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Solution

Similar to the question __[LeetCode 26] Remove Duplicates From Sorted Array__. Use 2 pointers. 

### Let's play a game

The code I gave is 21 lines. It's too long. Can we solve this problem with less code? 

Sure we can! I have a 10-line version: 

    public class Solution {
        public int removeElement(int[] A, int elem) {
            int left = 0, right = 0;
            while (right < A.length) {
                if (A[right] == elem) right++;
                else A[left++] = A[right++];
            }
            return left;
        }
    }

Now for a moment I thought the above code is the most concise, until I read [this blog](http://needjobasap.blogspot.sg/2014/01/removeelement-leetcode.html). The code is: 

    public class Solution {
        public int removeElement(int[] A, int elem) {
            int p = 0;
            for (int i = 0; i < A.length; i++)
                if (A[i] != elem) A[p++] = A[i];
            return p;
        }
    }

OK game over. Look at the standard answer below. Happy Leetcoding! 

### My code 

    public class Solution {
        public int removeElement(int[] A, int elem) {
            if (A == null || A.length == 0) {
                return 0;
            }
            int len = A.length;
            int left = 0;
            int right = 0;
            while (right < len) {
                // skip all instances of elem 
                while (right < len && A[right] == elem) {
                    right++;
                }
                if (right == len) {
                    break;
                }
                A[left++] = A[right++];
            }
            return left;
        }
    }
