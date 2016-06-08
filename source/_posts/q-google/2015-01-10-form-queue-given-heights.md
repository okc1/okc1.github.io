---
layout: post
title: "[Google] Form a Queue Given Heights "
comments: true
category: q-google
tags: [ src ]
---

### Question 

[link1](http://www.geeksforgeeks.org/reverse-a-stack-using-recursion/), [link2](http://www.weiming.info/zhuti/JobHunting/31903469/), [link3](http://www.mitbbs.com/article_t1/JobHunting/32856675_0_1.html#top). 

> There is an array of integers which represent heights of persons. 

> Given another array... Let's call it count-array. It contain how many persons in front of him are greater than him in height. 

> 求原数组。(原数组中元素是从1到n。)

> Example: 

    Input(Count array): 0, 0, 2, 0
    Output(原数组): 2, 3, 1, 4

> 求nlogn的算法。

### Solution

This is naive solution from floor 29 of [this thread](http://www.weiming.info/zhuti/JobHunting/31903469/): 

>总结一下，用一个List存放1...n。
>
>从头到尾扫描给定的数组，每得到一个值，从List里删掉。
>
>因为List里数据是有序的，因此remove操作可以使用二分法，复杂度为O(logn).
>
>这样本算法复杂度为O(nlogn).

Example: 

    count array 
    i C[0,0,2,0]   N[4, 3, 2, 1]
    3 C[3] = 0     在N里面删除N[0]=4, N=[3, 2, 1],   Ans=[4]
    2 C[2] = 2     在N里面删除N[2]=1, N=[3, 2],   Ans=[1, 4]
    1 C[1] = 0     在N里面删除N[0]=3, N=[2],   Ans=[3, 1, 4]
    0 C[0] = 0     在N里面删除N[0]=2, N=[], Ans=[2, 3, 1, 4]

But there is a problm here, since removing item from list requires O(n), we will achieve O(n^2) time. How do we optimize this? 

__The answer is BST__ with each node keeping track of how many nodes is on the left branch, and how many on right branch. For details of this type of TreeNode, refer to __[CC150v5] 11.8 Get Rank in Stream of Integers__. 

The conclusion: 

>可以化归为这样一道题：
>
>设计一个有序的数据结构，最初里头有自然数1到n这n个元素，
>
>随后这些元素可以被删除，但剩下元素仍然保持有序。
>
>要求实现方法GetKthElement(int k)和RemoveKthElemenet(int k)，
>
>使得它们在任意时刻都不超过O(lgN), N为当前的元素个数
>
>感觉要结合BST之类

### Code

Naive approach, O(n^2): 

	public int[] form(int peopleCount, int[] countArray) {
		int len = peopleCount;
		int[] heightQueue = new int[len];
		List<Integer> list = new ArrayList<Integer>();
		for (int i = peopleCount; i > 0; i--) {
			list.add(i);
		}
		for (int i = len - 1; i >= 0; i--) {
			heightQueue[i] = list.remove(countArray[i]);
		}
		return heightQueue;
	}
