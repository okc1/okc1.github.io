---
layout: post
title: "[Question] Get Max Number Game (minmax + dp) "
comments: true
category: Question

---

# Question 

[link](http://www.weiming.info/zhuti/JobHunting/31725587/)

> 两个人（A，B）参与一个游戏，规则如下：

> 1）一个随机的整数数列有偶数个数,a1,a2,...a2n
>
> 2）A 先从数列取数，但只能从两头取,a1 or a2n
>
> 3)然后Ｂ取数，也是只能从剩下的两头取，依此类推，两个人轮流，都只能从两头取
>
> Output __the max sum of numbers__ that player 1 is going to get. 

# Solution

This question can be solved with DP by using the following 3 equations: 

1. sum[i][j] sum of number from i to j
1. val[i][j]: the max value that can be obtained if only the range [i,j] is left and you take the move first
1. pos[][] is related to val[][], as it denotes whether we take i or j

After we got sum[][] array fully filled up, the transition equation of val[][] looks like: 

    val[x][y] = sum[x][y] - MIN( val[x+1][y], val[x][y-1] )

As for pos[][]:

    pos[x][y] = x  if val[x+1][y] < val[x][y-1]
                y  otherwise

# Code

	public int getMaxSumPlayerOne(int[] input) {
		int len = input.length;
		// sum[i][j] sum of number from i to j
		int[][] sum = new int[len][len];
		// val[i][j]: the max value that can be obtained if only
		// the range [i,j] is left and you take the move first
		int[][] val = new int[len][len];
		// pos is related to val, as it denotes whether we take i or j
		int[][] pos = new int[len][len];

		// 1. fill in sum[][]
		for (int x = 0; x < len; x++) {
			for (int y = x; y < len; y++) {
				if (x == y) {
					sum[x][y] = input[x];
				} else if (x == 0) {
					// fill up the first row in the sum[][] dp array
					sum[x][y] = sum[x][y - 1] + input[y];
				} else {
					// starting from the 2nd row, it's gonna make use of 1st row
					// x >= 1
					sum[x][y] = sum[0][y] - sum[0][x - 1];
				}
			}
		}

		// 2. fill in val[][] and pos[][]
		for (int x = len - 1; x >= 0; x--) {
			for (int y = x; y < len; y++) {
				if (x == y) {
					val[x][y] = input[x];
					pos[x][y] = x;
				} else {
					// when I choose either x or y, I look at what the opponent
					// is gonna get after my move, then chose the smaller
					// v[][] for the remaining part
					val[x][y] = sum[x][y] - Math.min(val[x + 1][y], val[x][y - 1]);
					pos[x][y] = val[x + 1][y] < val[x][y - 1] ? x : y;
				}
			}
		}
		this.printSteps(pos, len);
		return val[0][len - 1];
	}

# Testing

    Input {1, 4, 3, 2}
    Player 1 take position 3
    Player 2 take position 2
    Player 1 take position 1
    Player 2 take position 0
    max sum for player 1 is 6

    Input {7, 5, 2, 6, 9, 8, 3, 4}
    Player 1 take position 0
    Player 2 take position 1
    Player 1 take position 7
    Player 2 take position 6
    Player 1 take position 5
    Player 2 take position 4
    Player 1 take position 3
    Player 2 take position 2
    max sum for player 1 is 25
