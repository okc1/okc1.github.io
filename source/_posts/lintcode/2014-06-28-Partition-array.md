---
layout: post
title: "[LintCode] Partition Array"
comments: true
category: LintCode

---

### Question 

[link](http://www.lintcode.com/en/problem/partition-array/)

> Given an array "nums" of integers and an int "k", Partition the array (i.e move the elements in "nums") such that,

> 1. All elements < k are moved to the left
> 2. All elements >= k are moved to the right

> Return the partitioning Index, i.e the first index "i" nums[i] >= k.

> Example: If nums=[3,2,2,1] and k=2, a valid answer is 1.

### Analysis 

The solution is to keep swapping elements. It confuses me for a while, until I realize the swapping mechanism is actually not difficult. 

There's another question on leetcode "Sort Color", which is similar to this question (just partition twice). 

### Code

    public int partitionArray(ArrayList<Integer> nums, int k) {
	    //write your code here
		ArrayList<Integer> ans = new ArrayList<Integer>();
		if (nums == null || nums.size() == 0) {
			return ans;
		}
		int len = nums.size();
		int left = 0;
		int right = len - 1;
		while (left < right) {
			while (left < len && nums.get(left) < k) {
				left++;
			}
			while (right >= 0 && nums.get(right) >= k) {
				right--;
			}
			if (left > right) {
				break;
			} else {
				// swap 2 elements
				int temp = nums.get(left);
				nums.set(left, nums.get(right));
				nums.set(right, temp);
				left++;
				right--;
			}
		}
		// now return the correct value
		if (left == len) {
			return len;
		} else {
			return left;
		}
    }
