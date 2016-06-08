---
layout: post
title: "[CC150v4] 5.7 Find Missing Number "
comments: true
category: CC150v4

---

### Question

> An array A[1...n] contains all the integers from 0 to n except for one number which is missing. In this problem, we cannot access an entire integer in A with a single operation.

> The elements of A are represented in binary, and the only operation we can use to access them is “fetch the jth bit of A[i]”, which takes constant time. Write code to find the missing integer. Can you do it in O(n) time?

### Solution

__This is a difficult bit operation question__. 

The main thing to understand is, for a particular bit: 

> if the bit value of the removed number is 0, then count(0) <= count(1)

> if the bit value of the removed number is 1, then count(0) > count(1)

By using this principle, we can easily find the missing value for each bit. 

__However, we must know when to stop checking__. For example: 

> input: 000, 001, 011

We know that the last bit is 0, second last is 1. We shall stop here and return the result "010". If we did not stop, the result value would be "110", which is wrong. How this is handled is by __passing only half of the input list each time__, and we also add one condition at the beginning:

	if (list.size() == 0)
		return 0;

By doing this, we always limit the input list to a smaller range, until we finish finding all bits. 

### Code

__hard to write__

	public static int findMissing(List<BitInteger> list) {
		return helper(list, BitInteger.INTEGER_SIZE - 1);
	}

	private static int helper(List<BitInteger> list, int col) {
		if (list.size() == 0)
			return 0;
		List<BitInteger> zeroList = new ArrayList<BitInteger>();
		List<BitInteger> oneList = new ArrayList<BitInteger>();
		for (BitInteger bit : list) {
			if (bit.fetch(col) == 0) {
				zeroList.add(bit);
			} else {
				oneList.add(bit);
			}
		}
		if (zeroList.size() <= oneList.size()) {
			// this means the missing value contains a 0
			return helper(zeroList, col - 1) << 1;
		} else {
			// the missing value contains 1
			return helper(oneList, col - 1) << 1 | 1;
		}
	}
