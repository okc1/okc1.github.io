---
layout: post
title: "[Question] Interleave Positive and Negative Numbers "
comments: true
category: Question
tags: [ src ]
---

### Question

[link](http://mp.weixin.qq.com/s?__biz=MzA5MzE4MjgyMw==&mid=200355650&idx=1&sn=f94e87cb391fb12af9531cedb452dba1&key=d232b50733c41de56b96f855d9cdea5824f24c712e158651b45d7fe139a94610a7561da1fab0104e968592b01f2439d4&ascene=7&uin=MzM2NjQyNQ%3D%3D&pass_ticket=i7pJQweQbuRdnUFUt5cdOmapPc%2FDW6Xk40U7%2Bcg%2F0o8%3D)

> 给一个包含正负整数的数组，要求对这个数组中的数进行重新排列，使得其正负交替出现。首先出现负数，然后是正数，然后是负数。有多余的数的一方，就放在末尾。

> 如 [1, 2, 3, -4]->[-4, 1, 2, 3]，[1,-3,2,-4,-5]->[-3,1,-4,2,-5]. 要求使用O(1)的额外空间。

> 如果需要保持正数序列和负数序列各自原来的顺序，如何做？

> 如果不需要保持正数序列和负数序列各自原来的顺序，如何做？

### Solution

I only solve this question if we __do not have to keep the original ordering__. 

Basically, 2 pointers search from beginning to end. If there're more + than -, move the extra positive values to the back of the array. Vice versa. 

### Code

__written by me__

	public void solve(int[] A) {
		int len = A.length;
		int neg = 0;
		int pos = 1;
		while (neg < len || pos < len) {

			while (neg < len && A[neg] < 0) {
				neg += 2;
			}
			while (pos < len && A[pos] > 0) {
				pos += 2;
			}
			// neg points to a positive value
			// pos points to a negative value
			// swap them (if they're valid position)
			if (neg >= len && pos >= len) {
				return;
			} else if (neg >= len) {
				// neg is done, there's more - then +
				// put all negative values pointed by pos to the back
				int right = len - 1;
				if (right % 2 == 0) {
					right--;
				}
				while (pos < right) {
					while (pos < len && A[pos] > 0) {
						pos += 2;
					}
					while (right >= 0 && A[right] < 0) {
						right -= 2;
					}
					// pos point to a negative value, right to positive value
					if (pos > right) {
						break;
					} else {
						swap(A, pos, right);
					}
				}
				return;
			} else if (pos >= len) {
				// pos is done, there's more + then -
				int right = len - 1;
				if (right % 2 == 1) {
					right--;
				}
				while (neg < right) {
					while (neg < len && A[neg] < 0) {
						neg += 2;
					}
					while (right >= 0 && A[right] > 0) {
						right -= 2;
					}
					if (neg > right) {
						break;
					} else {
						swap(A, neg, right);
					}
				}
				return;
			} else {
				swap(A, neg, pos);
			}
		}
	}

	private void swap(int[] array, int a, int b) {
		int temp = array[a];
		array[a] = array[b];
		array[b] = temp;
	}
