---
layout: post
title: "[CC150v5] 9.7 Paint Fill in Map "
comments: true
category: CC150v5
tags: [ src ]
---

### Question

> Implement the "paint fill" function that one might see on many image editing programs. 

> That is, given a screen (represented by a two-dimensional array of colors), a point, and a new color, __fill in the surrounding area__ until the color changes from the original color. 

### Solution

This is a BFS/DFS question, very similar to __[LeetCode 130] Surrounded Regions__. 

__However, this question is not same as surrounding region__, because no temporary storage of state is needed, __and we DO NOT NEED TO keep track of the visited positions__! 

Why is this? 

1. This question, we simple change the color __from A to B__. 
1. Surrounding Region is __change A to B, and B to A__. 

That's why, the nature of 2 questions are different. 

Code 1 is my first solution, and Code 2 is doing a BFS and set color directly to expected value. This type of questions is highly frequent and sometimes may cause confusions. 

### Code

__my code 1__, with 'temp' state

	public static void PaintFill1(Color[][] screen, int posX, int posY,
			Color ncolor) {
		// the queue keeps the list of positions that I'm going to visit
		Queue<Position> q = new LinkedList<Position>();
		int len = screen.length;
		Color original = screen[posX][posY];
		// visited origin node first
		q.offer(new Position(posX, posY));
		while (!q.isEmpty()) {
			// visit positions in q one by one (mark color as 'Temp')
			Position p = q.poll();
			if (p.x < 0 || p.x >= len || p.y < 0 || p.y >= len) {
				// invalid pos coordinate
				continue;
			} else if (screen[p.x][p.y] == Color.Temp
					|| screen[p.x][p.y] != original) {
				continue;
			}
			screen[p.x][p.y] = Color.Temp;
			q.offer(new Position(p.x - 1, p.y));
			q.offer(new Position(p.x + 1, p.y));
			q.offer(new Position(p.x, p.y - 1));
			q.offer(new Position(p.x, p.y + 1));
		}
		// finish visiting all positions that's original color
		for (int i = 0; i < len; i++) {
			for (int j = 0; j < len; j++) {
				if (screen[i][j] == Color.Temp) {
					screen[i][j] = ncolor;
				}
			}
		}
	}

__my code 2__, without 'temp' state

	public static void PaintFill2(Color[][] screen, int posX, int posY,
			Color ncolor) {
		// the queue keeps the list of positions that I'm going to visit
		Queue<Position> q = new LinkedList<Position>();
		int len = screen.length;
		Color original = screen[posX][posY];
		// visited origin node first
		q.offer(new Position(posX, posY));
		while (!q.isEmpty()) {
			// visit positions in q one by one (mark color as 'Temp')
			Position p = q.poll();
			if (p.x < 0 || p.x >= len || p.y < 0 || p.y >= len) {
				// invalid pos coordinate
				continue;
			} else if (screen[p.x][p.y] != original) {
				continue;
			}
			screen[p.x][p.y] = ncolor;
			q.offer(new Position(p.x - 1, p.y));
			q.offer(new Position(p.x + 1, p.y));
			q.offer(new Position(p.x, p.y - 1));
			q.offer(new Position(p.x, p.y + 1));
		}
	}
