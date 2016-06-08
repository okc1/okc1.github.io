---
layout: post
title: "[Google] Top n values from Sum of 2 arrays "
comments: true
category: q-google
tags: [ src ]
---

### Question 

[link](http://www.careercup.com/question?id=3213705)

> 给定两个数组A，B，长度均为n，求A[0]+B[0],…,A[0]+B[n-1],…,A[n-1]+B[0],…,A[n-1]+B[n]总共n^2个数的最大的n个值。

### Solution

Use a Heap and then iteratively pop 1 and push 2 elements. Until n values has been filled. 

### Code

	public int[] topN(int[] arr1, int[] arr2, int n) {
		int[] ans = new int[n];
		int index = n - 1;

		PriorityQueue<Pair> heap = new PriorityQueue<Pair>(n,
				new SpecialComparator(arr1, arr2));
		Arrays.sort(arr1);
		Arrays.sort(arr2);

		Pair maxPair = new Pair(n - 1, n - 1);
		heap.add(maxPair);

		for (int i = 0; i < n; i++) {
			Pair next = heap.poll();
			ans[index--] = arr1[next.x] + arr2[next.y];
			if (next.y - 1 >= 0) {
				heap.add(new Pair(next.x, next.y - 1));
			}
			if (next.x - 1 >= 0) {
				heap.add(new Pair(next.x - 1, next.y));
			}
		}
		return ans;
	}

	class SpecialComparator implements Comparator<Pair> {

		int[] arr1, arr2;

		public SpecialComparator(int[] a1, int[] a2) {
			arr1 = a1;
			arr2 = a2;
		}

		@Override
		public int compare(Pair p1, Pair p2) {
			// note that larger value shall go up top of the heap, so -1 * ...
			return -1 * (arr1[p1.x] + arr2[p1.y] - arr1[p2.x] - arr2[p2.y]);
		}
	}
