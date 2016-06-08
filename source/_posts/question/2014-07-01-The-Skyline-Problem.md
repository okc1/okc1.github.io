---
layout: post
title: "[Question] The Skyline Problem"
comments: true
category: Question

---

### Question 

[link](http://www.algorithmist.com/index.php/UVa_105)

> Given n buildings, each building is an rectangle located on 
x-axis, and indicated by (x1, x2, height). Calculate the 
outline of all buildings. Output them in order.

### Solution

__Solution 1 is keeping a heightmap (Brute force)__. Keep an array of a certain size, and update max_height for every single point. 

__Solution 2 is using Sweeping line algorithm__. Sweep from left to right, always try to find the largest height of the rectangle. 

First make sure the rectangles are sorted. While sweeping, if sees an building-start, insert the height to the heap. If a building-end, remove from the heap. Then the current maximum height is the max point in the heap. A visualized explanation can be found [here](https://briangordon.github.io/2014/08/the-skyline-problem.html). 

Total cost is O(nlogn), [source](http://qr.ae/Yt74m). 

__Two solutions compared__: 

1. In the brute force approach, doubling the width of the buildings will double the runtime cost. With the sweep line algorithm, it won't. 

1. Sweep Line algorithm will work if the input is not discrete, whereas the heightmap approach requires integer coordinates.

__Updated on Feb 1st, 2015__: using floor 26 of [this post](http://www.mitbbs.com/article_t1/JobHunting/32569901_0_2.html), we can do insertion and deletion in max-heap, then peek the largest element in the heap. 

> 把所有的turning points 放在一起，根据coordination从小到大sort 。

> 再用max-heap, 把所有的turning points扫一遍，遇到start turning point, 把 
volume放入max-heap. 遇到end turning point，把对应的volume从max-heap中取出。 

> max-heap的max 值就是对应区间的最大volume

Code presented below. 

### Code

Brate force code from [ucf](http://www.cs.ucf.edu/~dmarino/ucf/java/Skyline.java): 

	public static void main(String[] args) throws IOException {

		Scanner fin = new Scanner(new File("skyline.in"));

		// Read in general information about the buildings and skyline.
		int numbuildings = fin.nextInt();
		int min = fin.nextInt();
		int max = fin.nextInt();
		int size = max - min;

		// Initialize the skyline.
		int[] mysky = new int[size];
		for (int i = 0; i < size; i++)
			mysky[i] = 0;

		// For each building, edit the skyline as necessary.
		for (int i = 0; i < numbuildings; i++) {
			int left = fin.nextInt();
			int height = fin.nextInt();
			int right = fin.nextInt();

			// Note how we have to offset the left and right boundaries
			// due to how we set up our array. Basically, at each segment
			// of the skyline that the current building is part of, we see
			// if this current building is the tallest of the ones there.
			// If so, we make the necessary update.
			for (int j = left - min; j < right - min; j++)
				if (height > mysky[j])
					mysky[j] = height;
		}

		// Beginning of the skyline.
		System.out.print(min + " ");
		int cnt = 0;

		// Keep on going until you get right before the end of the skyline.
		while (cnt < size - 1) {

			// Increment cnt as long as the height is the same.
			while (cnt < size - 1 && mysky[cnt] == mysky[cnt + 1])
				cnt++;

			// Print out information for this part of the skyline.
			System.out.print(mysky[cnt] + " " + (cnt + 1 + min) + " ");
			cnt++;
		}

		// This is the case where the last segment is unique.
		if (cnt == size - 1)
			System.out.print(mysky[size - 1] + " " + max);
		System.out.println();
		fin.close();
	}

The heap solution:

	public int[] skyline(List<Building> bds, int min, int max) {
		int[] output = new int[max - min];

		List<Edge>[] edges = new List[max - min];
		for (int i = 0; i < edges.length; i++) {
			edges[i] = new ArrayList<Edge>();
		}
		for (Building b : bds) {
			// put all edges into an array of edges
			edges[b.from].add(new Edge(b, true));
			edges[b.to].add(new Edge(b, false));
		}

		Queue<Building> heap = new PriorityQueue<Building>(100,
				new Comparator<Building>() {
					public int compare(Building b1, Building b2) {
						return b2.height - b1.height;
					}
				});
		for (int i = 0; i < edges.length; i++) {
			// insert or remove each building at position i into max heap
			for (Edge e : edges[i]) {
				if (e.isEnter) {
					heap.add(e.building);
				} else {
					heap.remove(e.building);
				}
			}
			// then culculate the current hight, which is top of the heap
			if (!heap.isEmpty()) {
				output[i] = heap.peek().height;
			}
		}

		return output;
	}

	static class Edge {
		Building building;
		boolean isEnter;

		public Edge(Building bld, boolean enter) {
			building = bld;
			isEnter = enter;
		}
	}

	static class Building {
		int from;
		int to;
		int height;

		public Building(int a, int b, int c) {
			from = a;
			to = b;
			height = c;
		}
	}
