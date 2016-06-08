---
layout: post
title: "[LeetCode 136] Single Number"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/single-number/)

<div class="question-content bg-color bg-img font-color">
            <p class="font-color"></p><p class="font-color">Given an array of integers, every element appears <i>twice</i> except for one. Find that single one.</p>

<p class="font-color">
<b>Note:</b><br>
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?
</p><p class="font-color"></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__First solutions is bit manipulation__. 

> If two numbers are the same, then XOR result is 0. 

And for negative integers: 

> A negative number is a [bit field](http://en.wikipedia.org/wiki/Bit_field) just like a positive number. XOR doesn't care

Follow-up question, what if the input is not an array in interger, but a bunch of Strings? [This guy](http://stackoverflow.com/a/35271) have the answer. 

> There are ways of XORing strings by XORing the individual chars - you would just have to have a temporary variable as large as the largest string. 

> What wouldn't work is trying to XOR a linked list or some other complicated data structure. 

Which is to say, a string is just like an array of chars (integers). For every char (integer), just apply the same method and we shall have the answer. 

__Second solution is HashSet__, but must use more space. Code is posted below as well. 

Someone also sort then find, but this takes more time. 

### Code

__First, XOR solution__

    public int singleNumber(int[] A) {
        int num = A[0];
        for (int i = 1; i < A.length; i ++)
            num = num ^ A[i];
        return num;
    }

__Second, HashSet solution__

The last line "return -1" is only for compiling purposes, and will not be executed. 

    public int singleNumber(int[] A) {
        HashSet<Integer> set = new HashSet<Integer>();
        for (int i = 0; i < A.length; i ++) {
            if (set.contains(A[i]))
                set.remove(A[i]);
            else
                set.add(A[i]);
        }
        for (Integer a: set)
            return a;
		return -1;
    }
