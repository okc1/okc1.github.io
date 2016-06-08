---
layout: post
title: "[CC150v5] 9.10 Stack up the Boxes "
comments: true
category: CC150v5
tags: [ src ]
---

### Question

> You have a stack of n boxes, with widths w., heights h, and depths d. The boxes can only be stacked on top of one another if each box is strictly larger than the box above it in width, height, and depth. 

> Implement a method to build the tallest stack possible, where the height of a stack is the sum of the heights of each box. 

### Solution

This is appearantly a DP question. I did it in the normal way, and the solution turns out to be very good: 

	DP solution is        2638ms
	Recursive solution is 1322ms
	My solution is         370ms

I could not understand the 2 solutions given in the book. Sorry.

The coding is a bit lengthy, and we keeps 2 DP arrays. __Not an easy question of course__, but the solution is actually standard. 

### Code

	public static ArrayList<Box> createStack(Box[] boxes) {
		ArrayList<Box> ans = new ArrayList<Box>();
		int len = boxes.length;
		int[] heights = new int[len];
		int[] preMap = new int[len];
		int maxIndex = 0;

		// start DP
		for (int i = 0; i < len; i++) {
			heights[i] = boxes[i].height;
			preMap[i] = -1;
			for (int j = 0; j < i; j++) {
				if (boxes[j].canBeAbove(boxes[i])) {
					int newHeight = heights[j] + boxes[i].height;
					if (newHeight > heights[i]) {
						heights[i] = newHeight;
						preMap[i] = j;
					}
				}
			}
			// now updated maxIndex
			if (heights[i] > heights[maxIndex]) {
				maxIndex = i;
			}
		}

		// print from maxIndex all the way backwards
		while (maxIndex != -1) {
			ans.add(boxes[maxIndex]);
			// the print order is reversed, so...
			maxIndex = preMap[maxIndex];
		}
		return ans;
	}
