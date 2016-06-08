---
layout: post
title: "[Google] Continental divider "
comments: true
category: q-google

---

### Question 

[link](http://www.mitbbs.com/article_t1/JobHunting/32882153_0_1.html)

> 给一个矩阵，其中0代表海洋，其他数字代表高度，秉着水往低处流的原则，求出能够流向任意海洋的点。 比如说

    0 0 0 1 2 3 0
    0 1 2 2 4 3 2
    2 1 1 3 3 2 0
    0 3 3 3 2 3 3

> 那么就要给出 第二行的4 （这有这点出发，能够找到连通道四个0的区域的一条__非递增
路线__），当然也有可能找不到这样的点，或者找到多个点。

### Solution 

I read online and the best solution I come up with is Brute Force. I did not really understand the [online discussions](http://www.mitbbs.com/article_t1/JobHunting/32882153_0_1.html). 

So if you are reading this and want to discuss with me, kindly leave me a comment! 

### Code

brute force

	public void findSuperPeak(int[][] map) {
		int m = map.length;
		int n = map[0].length;
		for (int i = 0; i < m; i++) {
			for (int j = 0; j < n; j++) {
				if (check(map, new Pair(i, j), m, n)) {
					System.out.println("Found point (" + i + ", " + j
							+ ") with height of " + map[i][j]);
				}
			}
		}
	}

	private boolean check(int[][] originalMap, Pair p, int m, int n) {
		// check if point can flow to all oceans
		if (originalMap[p.x][p.y] == 0) {
			return false;
		}

		int[][] map = new int[m][n];
		for (int i = 0; i < m; i++) {
			for (int j = 0; j < n; j++) {
				map[i][j] = originalMap[i][j];
			}
		}

		Queue<Pair> q = new LinkedList<Pair>();
		q.offer(p);

		while (!q.isEmpty()) {
			Pair top = q.poll();
			int x = top.x;
			int y = top.y;
			if (map[x][y] == -1) {
				continue;
			}
			// add neighbor nodes who are visitable from here
			if (x - 1 >= 0 && map[x - 1][y] <= map[x][y]) {
				// water can flow from:
				// 1. high altitude to lower
				// 2. from ocean to ocean
				q.offer(new Pair(x - 1, y));
			}
			if (x + 1 < m && map[x + 1][y] <= map[x][y]) {
				q.offer(new Pair(x + 1, y));
			}
			if (y - 1 >= 0 && map[x][y - 1] <= map[x][y]) {
				q.offer(new Pair(x, y - 1));
			}
			if (y + 1 < n && map[x][y + 1] <= map[x][y]) {
				q.offer(new Pair(x, y + 1));
			}

			// visit this point
			map[x][y] = -1;
		}

		// now we finished BFS and the entire map with lower altitude is visited
		// (including all ocean points). We now check if there exists a 0 in map
		for (int[] arr : map)
			for (int i : arr)
				if (i == 0) // found an unvisited ocean point
					return false;
		return true;
	}
