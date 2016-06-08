---
layout: post
title: "[CC150v5] 5.5 Calculate Bits Conversion Required "
comments: true
category: CC150v5
tags: [ src ]
---

### Question

> Write a function to determine the number of bits (change) required to convert integer A to integer B. 

### Solution

Using XOR operation, we can find out number of bits that are different. 

The next important thing is to know __how to count the number of '1's in a integer__. It's like this: 

> c = c & (c - l) clears the least significant bit of '1'. 
>
> Keep doing this until all '1's are cleared. 

### Code

__code 1__

	public static int calcBitsSwapMe1(int a, int b) {
		int num = a ^ b;
		int count = 0;
		while (num != 0) {
			count += num & 1;
			num = num >>> 1;
		}
		return count;
	}

__code 2__

	public static int calcBitsSwapMe2(int a, int b) {
		int num = a ^ b;
		int count = 0;
		while (num != 0) {
			num = num & (num - 1);
			count++;
		}
		return count;
	}
