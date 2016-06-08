---
layout: post
title: "[Amazon] Mininum Range that includes at least One "
comments: true
category: Question

---

### Question

[link](http://www.careercup.com/question?id=5103437989543936)

> There are many sorted arrays. Find a minimum range, so that in each array there's at least one integer within this range.

### Solution

__Min-heap__. [source](http://www.careercup.com/question?id=16759664)

> There are k lists of sorted integers. Make a min heap of size k containing 1 element from each list. Keep track of min and max element and calculate the range. 

> In min heap, minimum element is at top. Delete the minimum element and another element instead of that from the same list to which minimum element belong. Repeat the process till any one of the k list gets empty. 

### Code 

	public void printMinRange(int[][] input) {
		Comparator<Pointer> compr = new HeapComparator(input);
		// Note that we pass in 'input' arrays to the comparator
		PriorityQueue<Pointer> heap = new PriorityQueue<Pointer>(SIZE, compr);

		int maxVal = Integer.MIN_VALUE;
		for (int i = 0; i < SIZE; i++) {
			heap.add(new Pointer(i, 0));
			// insert the head of each array into the heap
			maxVal = Math.max(maxVal, input[i][0]);
			// keep additional value to keep track of the max value in heap
		}

		int left = 0;
		int right = Integer.MAX_VALUE;
		while (heap.size() == SIZE) {
			Pointer p = heap.remove();
			// first, update the range
			if (maxVal - input[p.index][p.position] < right - left) {
				right = maxVal;
				left = input[p.index][p.position];
			}
			// then, push the next element after 'p' to the heap
			// meanwhile, update 'maxVal'
			if (p.position + 1 < input[p.index].length) {
				Pointer nextP = new Pointer(p.index, p.position + 1);
				heap.add(nextP);
				maxVal = Math.max(maxVal, input[nextP.index][nextP.position]);
			}
			// when 'p' is the last element in the row, terminate loop
		}
		System.out.println("Left boundary: " + left);
		System.out.println("Right boundary: " + right);
	}

	class HeapComparator implements Comparator<Pointer> {

		int[][] arrays = null;

		public HeapComparator(int[][] input) {
			arrays = input;
		}

		public int compare(Pointer p1, Pointer p2) {
			return arrays[p1.index][p1.position]
					- arrays[p2.index][p2.position];
		}
	}

	class Pointer {
		int index, position;

		public Pointer(int x, int y) {
			index = x;
			position = y;
		}
	}
