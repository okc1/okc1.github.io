---
layout: post
title: "[Google] Winner of tic-tac-toe"
comments: true
category: q-google
tags: [ src ]
---

### Question 

[link](http://www.glassdoor.com/Interview/How-would-you-determine-if-someone-has-won-a-game-of-tic-tac-toe-on-a-board-of-any-size-QTN_1104.htm)

> How would you determine if someone has won a game of tic-tac-toe on a board of any size? 

(This is also on CC150v4 19.2 and CC150v4 17.2)

### Solution

First, confirm that when the number of pieces in a line equals to the dimension of the board, one person wins. Eg. for 10 * 10 board, 10 pieces need to be in 1 line. 

__[We can determine](http://www.glassdoor.com/Interview/How-would-you-determine-if-someone-has-won-a-game-of-tic-tac-toe-on-a-board-of-any-size-QTN_1104.htm) if someone has won during a game in real time__, as in checking after every move. 

> Create an array of size 2n+2 at the beginning of the game and fill it with zeros. Each spot in the array will be a sum of X's or O's horizontally (the first n places in the array), vertically (the second n places in the array) and diagonally (the last 2 places). Then with every move, you add 1 to the 2 places (or 3 if on a diagnol) of the array if X, and subtract 1 if its an O. After adding you check and see if the value of the array is equal to n or -n, if it is, n mean X has won and -n means O has won.

This is uses O(2n+2) space, but it's the best solution I can find online. I wrote code posted below. 

### Code

__written by me__

	enum Piece {
		Empty, Red, Blue
	};
    
	public static Piece hasWon3(Piece[][] board) {

		int N = board.length;

		// O(2n+2) space to store count info
		int[] rowCnt = new int[N];
		int[] colCnt = new int[N];
		int[] digCnt = new int[2];

		for (int i = 0; i < N; i++) {
			for (int j = 0; j < N; j++) {

				int pieceValue = 0;
				if (board[i][j] == Piece.Blue) {
					pieceValue = 1;
				} else if (board[i][j] == Piece.Red) {
					pieceValue = -1;
				}

				// if empty, pieceValue is 0
				// if blue, add 1 in count
				// if red, subtract 1 in count
				rowCnt[i] += pieceValue;
				if (checkFinish(rowCnt[i], N) != null) {
					return checkFinish(rowCnt[i], N);
				}

				// after adding the count, check if the game finishes
				colCnt[j] += pieceValue;
				if (checkFinish(colCnt[j], N) != null) {
					return checkFinish(colCnt[j], N);
				}

				if (i == j) {
					digCnt[0] += pieceValue;
					if (checkFinish(digCnt[0], N) != null) {
						return checkFinish(digCnt[0], N);
					}
				} else if (i + j == N) {
					digCnt[1] += pieceValue;
					if (checkFinish(digCnt[1], N) != null) {
						return checkFinish(digCnt[1], N);
					}
				}
			}
		}
		// game not finished, continue
		return Piece.Empty;
	}

	private static Piece checkFinish(int count, int N) {
		if (count == N)
			return Piece.Blue;
		else if (count == -1 * N)
			return Piece.Red;
		else
			return null;
	}
