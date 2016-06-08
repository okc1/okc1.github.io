---
layout: post
title: "[Google] Shortest Manhattan Distance "
comments: true
category: q-google

---

### Question 

[link](http://www.mitbbs.com/article_t/JobHunting/33054861.html)

> 给一个 n*m 的房间，房间里存在各种可能的墙，房间的格子里已经放了 e 个器材，要
求新放一个器材，放置位置距其它 e 个器材的距离最近。Breadth-first search.

### Solution 

> 对 e个设备 BFS, 求每个设备到每个可以放新器材的点的距离，然后叠加。

> 最后O（n^2）一遍找最小值。复杂度O（e*n^2）

As for whether we choose to check each equipment position, or check each vacant position, it's decided by how many equipment is there. If very little equipments (e is small), then this solution should work.

However, what is there is obstacles in the matrix?

We have to use BFS then. It took more space usage, but the time complexity should be same. 

### Code

	public void findCenter(int[][] input, int numberOfEquip) {
		int m = input.length;
		int n = input[0].length;
		
		// there's gonna be m * n positions
		// we gonna cumulate (numberOfEquip) distances for each position
		int[] dis = new int[m * n];
		
		// from the input map, find Equipments
		for (int i = 0; i < m; i++) {
			for (int j = 0; j < n; j++) {
				if (input[i][j] == 1) {
					// 1 represents equipment
					// when found, add the distance to every position
					cumulateDistance(i, j, dis, m, n);
				}
			}
		}
		
		// find the smallest cumulated distance from dis[].
		int sIndex = 0;
		int smallest = dis[0];
		for (int i = 0; i < m * n; i++) {
			if (dis[i] < smallest) {
				smallest = dis[i];
				sIndex = i;
			}
		}
		
		// index sIndex is the final answer
		System.out.println("Answer: " + (sIndex / n) + " " + (sIndex % n));
	}
	
	private void cumulateDistance(int x, int y, int[] dis, int m, int n) {
		for (int i = 0; i < m * n; i++) {
			int a = i / n;
			int b = i % n;
			dis[i] += Math.abs(a - x) + Math.abs(b - y);
		}
	}
