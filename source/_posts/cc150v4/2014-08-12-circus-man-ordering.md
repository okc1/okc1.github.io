---
layout: post
title: "[CC150v4] 9.7 Circus Tower Routine"
comments: true
category: CC150v4
tags: [ src ]
---

### Question 

> A circus is designing a tower routine consisting of people standing atop one another’s shoulders. For practical and aesthetic reasons, each person must be both shorter and lighter than the person below him or her. Given the heights and weights of each person in the circus, write a method to compute the largest possible number of people in such a tower.

> EXAMPLE:

>Input: (ht, wt): (65, 100) (70, 150) (56, 90) (75, 190) (60, 95) (68, 110)
>
> Output: The longest tower is length 6 and includes from top to bottom: (56, 90) (60,95) (65,100) (68,110) (70,150) (75,190)

### Solution

The solution given in the book is unclear, but it's a very simple idea which is pointed out [here](http://www.careercup.com/question?id=9339758) and [here](http://hawstein.com/posts/9.7.html). 

1. sort the input persons by 'height'. O(nlogn) 
2. find the longest increasing 'weight' sequence in the sorted list. This can be done in O(nlogn) with DP.

### Code

__written by me__

	public int longestTower(List<Man> list) {
		Collections.sort(list, new ManComparator());
		// now find the longest increasing sequence of 'weight' property
		int len = list.size();
		int maxLen = 1;
		int[] dp = new int[len];
		for (int i = 1; i < len; i++) {
			dp[i] = 1;
			for (int j = 0; j < i; j++) {
				if (list.get(i).weight > list.get(j).weight) {
					dp[i] = Math.max(dp[i], dp[j] + 1);
				}
			}
			maxLen = Math.max(maxLen, dp[i]);
		}
		return maxLen;
	}

	class ManComparator implements Comparator<Man> {
		@Override
		public int compare(Man o1, Man o2) {
			return o1.height - o2.height;
		}
	}
