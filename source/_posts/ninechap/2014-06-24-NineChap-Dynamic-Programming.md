---
layout: post
title: "[NineChap 5.1] Dynamic Programming"
comments: true
category: NineChap

---


## Dynamic Programming

The fundamental of DP is 'merorized search'. It's easy to implement but bad for memory. And it's generally useless in the industry. 

### When to use DP?

1. Input cannot sort
1. Find minimum/maximum result
1. Check the feasibility
1. Count all possible solutions

If question asks you to find all possible solutions, it's gonna be DFS, not DP. 

### 5 Types of DP

1. Matrix DP (10%)
2. Sequence/Two Sequences DP (80%)
3. Interval DP (5%)
4. Tree DP (5%)
5. States Compressing DP (0%)

Type 3 to 5 are less important. 

### Question List

__Type 1: Matrix DP__

1. __[Triangle]({% post_url /leetcode/2014-05-27-Triangle %})__

1. __[Unique Paths ]({% post_url /leetcode/2014-05-20-Unique-Paths %})__

1. __[Unique Paths II  ]({% post_url /leetcode/2014-05-20-Unique-Paths-II %})__

1. __[Minimum Path Sum ]({% post_url /leetcode/2014-05-20-Minimum-Path-Sum %})__

__Type 2.1: Sequence Dp__

1. __[Climbing Stairs ]({% post_url /leetcode/2014-05-21-Climbing-Stairs %})__

1. __[Jump Game ]({% post_url /leetcode/2014-05-16-Jump-Game %})__

1. __[Jump Game II]({% post_url /leetcode/2014-05-14-Jump-Game-II %})__ - tricky, index handling

1. __[Palindrome Partitioning II ]({% post_url /leetcode/2014-05-30-Palindrome-Partitioning-II %})__

1. __[Word Break ]({% post_url /leetcode/2014-06-02-Word-Break %})__

1. __[Word Break II]({% post_url /leetcode/2014-06-02-Word-Break-II %})__

1. __[Decode Ways ]({% post_url /leetcode/2014-05-23-Decode-Ways %})__ - tricky, initial state

1. __[Longest Increasing Subsequence]({% post_url /lintcode/2014-06-24-Longest-Increasing-Subsequence %})__

__Type 2.2: Two Sequences Dp__

1. __[Distinct Subsequences ]({% post_url /leetcode/2014-05-27-Distinct-Subsequences %})__ - difficult, state transition formula

1. __[Edit Distance ]({% post_url /leetcode/2014-05-21-Edit-Distance %})__

1. __[Interleaving String ]({% post_url /leetcode/2014-05-24-Interleaving-String %})__

1. __[Longest Common Subsequence]({% post_url /lintcode/2014-06-24-Longest-Common-Subsequence %})__

__Type 3: Interval Dp__

[Merge Stone](http://wikioi.com/problem/1048/)

__Type 4: Tree Dp__

1. __[Binary Tree Maximum Path Sum]({% post_url /leetcode/2014-05-28-Binary-Tree-Maximum-Path-Sum %})__

__Type 5: States Compressing DP__

Ignore. 

Additional questions

1. __[Maximum Subarray ]({% post_url /leetcode/2014-05-20-Maximum-Subarray %})__

1. __[Coin Change Problem]({% post_url /question/2014-06-30-Coin-Changing-Problem %})__

## Code

#### Type 1: Matrix DP

__Triangle__

    public int minimumTotal(List<List<Integer>> triangle) {
        if (triangle == null || triangle.size() == 0) {
            return 0;
        }
        int len = triangle.size();
        int[][] dp = new int[len][len];
        for (int i = len - 1; i >= 0; i--) {
            // bottom-up approach (row by row)
            for (int j = 0; j <= i; j++) {
                if (i == len - 1) {
                    dp[i][j] = triangle.get(i).get(j);
                } else {
                    dp[i][j] = triangle.get(i).get(j)
                            + Math.min(dp[i+1][j], dp[i+1][j+1]);
                }
            }
        }
        return dp[0][0];
    }

__Unique Paths__

    public int uniquePaths(int m, int n) {
        if (m == 0 && n == 0) {
            return 0;
        }
        int[][] dp = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (i == 0 || j == 0) {
                    dp[i][j] = 1;
                } else {
                    dp[i][j] = dp[i-1][j] + dp[i][j-1];
                }
            }
        }
        return dp[m-1][n-1];
    }

__Unique Paths II__

    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        if (obstacleGrid == null) {
            return 0;
        }
        int m = obstacleGrid.length;
        int n = obstacleGrid[0].length;
        int[][] dp = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (obstacleGrid[i][j] != 0) {
                    dp[i][j] = 0;
                } else if (i == 0 && j == 0) {
                    dp[i][j] = 1;
                } else if (i == 0) {
                    dp[i][j] = dp[i][j-1];
                } else if (j == 0) {
                    dp[i][j] = dp[i-1][j];
                } else {
                    dp[i][j] = dp[i-1][j] + dp[i][j-1];
                }
            }
        }
        return dp[m-1][n-1];
    }

__Minimum Path Sum__

    public int minPathSum(int[][] grid) {
        if (grid == null) {
            return 0;
        }
        int m = grid.length;
        int n = grid[0].length;
        int[][] dp = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (i == 0 && j == 0) {
                    dp[i][j] = grid[i][j];
                } else if (i == 0) {
                    dp[i][j] = dp[i][j-1] + grid[i][j];
                } else if (j == 0) {
                    dp[i][j] = dp[i-1][j] + grid[i][j];
                } else {
                    dp[i][j] = grid[i][j] + Math.min(dp[i-1][j], dp[i][j-1]);
                }
            }
        }
        return dp[m-1][n-1];
    }

#### Type 2.1: Sequence Dp

__Climbing Stairs__

    public int climbStairs(int n) {
        if (n <= 2) {
			return n;
		}
		int[] dp = new int[n];
		dp[0] = 1;
		dp[1] = 2;
		for (int i = 2; i < n; i++) {
			dp[i] = dp[i - 2] + dp[i - 1];
		}
		return dp[n - 1];
    }

__Jump Game__

    public boolean canJump(int[] A) {
        if (A == null || A.length == 0) 
			return false;
		int reach = 0;
		int len = A.length;
		for (int i = 0; i < len; i++) {
			if (i > reach) 
				break;
			reach = Math.max(reach, i + A[i]);
			if (reach >= len - 1) 	
				return true;
		}
		return false;
    }

__Jump Game II__

    public int jump(int[] A) {
        if (A == null || A.length <= 1) 
			return 0;
		int[] dp = new int[A.length];
		int cur = 1;
		for (int i = 0; i < A.length - 1; i++) {
			while (cur <= i + A[i] && cur < dp.length) {
				dp[cur] = dp[i] + 1;
				cur++;
			}
			if (cur == dp.length) {
				break;
			}
		}
		return dp[A.length - 1];
    }

__Palindrome Partitioning II__

    public int minCut(String s) {
        if (s == null || s.length() <= 1) {
            return 0;
        }
        boolean[][] map = palindromeMap(s);
        int len = s.length();
        int[] dp = new int[len + 1];
        dp[0] = -1;
        for (int i = 1; i <= len; i++) {
            dp[i] = Integer.MAX_VALUE;
            for (int j = 1; j <= i; j++) {
                if (map[i-1][j-1]) {
                    dp[i] = Math.min(dp[i], dp[j-1] + 1);
                }
            }
        }
        return dp[len];
    }
    
    private boolean[][] palindromeMap(String s) {
        int len = s.length();
        boolean[][] map = new boolean[len][len];
        char[] ss = s.toCharArray();
        for (int i = 0; i < len; i++) {
            for (int j = i; j >= 0; j--) {
                if (i == j) {
                    map[i][j] = true;
                } else if (i - j == 1) {
                    map[i][j] = ss[i] == ss[j];
                } else {
                    map[i][j] = (ss[i] == ss[j]) & map[i - 1][j + 1];
                }
            }
        }
        return map;
    }

__Word Break__

    public boolean wordBreak(String s, Set<String> dict) {
        if (s == null || s.length() == 0) {
            return true;
        }
        int len = s.length();
        boolean[] dp = new boolean[len + 1];
        dp[0] = true;
        for (int i = 1; i <= len; i++) {
            for (int j = 0; j < i; j++) {
                if (!dp[j]) {
                    continue;
                }
                if (dict.contains(s.substring(j, i))) {
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[len];
    }

__Word Break II__

My code is definitely correct, although it got TLE. 

See original post for more. 

__Decode Ways__

    public int numDecodings(String s) {
        if (s == null || s.length() == 0) {
			return 0;
		}
		int len = s.length();
		int[] dp = new int[len + 1];
		dp[0] = 1;
		dp[1] = 1; // pay attention to the initial state
		if (!isValidNumber(s.substring(0, 1))) {
			return 0;
		}
		for (int i = 2; i <= len; i++) {
			if (isValidNumber(s.substring(i - 1, i))) {
				dp[i] += dp[i - 1];
			}
			if (isValidNumber(s.substring(i - 2, i))) {
				dp[i] += dp[i - 2];
			}
		}
		return dp[len];
    }
	
	private boolean isValidNumber(String input) {
		if (input.length() == 0 || input.length() > 2 || input.charAt(0) == '0') {
			return false;
		}
		int num = Integer.parseInt(input);
		return (1 <= num && num <= 26);
	}

__Longest Increasing Subsequence__

There's a new post in 'Lintcode' category. 

#### Type 2.2: Two Sequences Dp

__Distinct Subsequences__

    public int numDistinct(String S, String T) {
        int m = S.length(), n = T.length();
        int[][] dp = new int[m + 1][n + 1];
        for (int i = 0; i <= m; i++) {
            for (int j = 0; j <= n; j++) {
                if (j == 0) {
                    dp[i][j] = 1;
                } else if (i == 0) {
                    dp[i][j] = 0;
                } else {
                    dp[i][j] = dp[i - 1][j];
                    if (S.charAt(i - 1) == T.charAt(j - 1)) {
                        dp[i][j] += dp[i - 1][j - 1];
                    }
                }
            }
        }
        return dp[m][n];
    }

__Edit Distance__

    public int minDistance(String A, String B) {
        if (A == null || B == null)
            return 0;
        int m = A.length(), n = B.length();
        int[][] dp = new int[m + 1][n + 1];
        for (int i = 0; i <= m; i++) {
            for (int j = 0; j <= n; j++) {
                if (i == 0) {
                    dp[i][j] = j;
                } else if (j == 0) {
                    dp[i][j] = i;
                } else {
                    if (A.charAt(i - 1) == B.charAt(j - 1)) {
                        dp[i][j] = dp[i - 1][j - 1];
                    } else {
                        dp[i][j] = Math.min(dp[i - 1][j - 1], dp[i - 1][j]);
                        dp[i][j] = Math.min(dp[i][j], dp[i][j - 1]);
                        dp[i][j]++;
                    }
                }
            }
        }
        return dp[m][n];
    }

__Interleaving String__

    public boolean isInterleave(String s1, String s2, String s3) {
        if (s1 == null || s2 == null) {
            return false;
        }
        int m = s1.length(), n = s2.length();
        if (m + n != s3.length()) {
            return false;
        }
        boolean[][] dp = new boolean[m + 1][n + 1];
        for (int i = 0; i <= m; i++) {
            for (int j = 0; j <= n; j++) {
                if (i == 0) {
                    dp[i][j] = s2.substring(0, j).equals(s3.substring(0, j));
                    continue;
                } else if (j == 0) {
                    dp[i][j] = s1.substring(0, i).equals(s3.substring(0, i));
                    continue;
                }
                if (i > 0 && dp[i - 1][j]
                        && s1.charAt(i - 1) == s3.charAt(i + j - 1)) {
                    dp[i][j] = true;
                }
                if (j > 0 && dp[i][j - 1]
                        && s2.charAt(j - 1) == s3.charAt(i + j - 1)) {
                    dp[i][j] = true;
                }
            }
        }
        return dp[m][n];
    }

__Longest Common Subsequence__

There's a new post in 'Lintcode' category. 

### Type 3: Interval Dp

__Merge Stone__

>有n堆石子排成一列，每堆石子有一个重量w[i], 每次合并可以合并相邻的两堆石子，一次合并的代价为两堆石子的重量和w[i]+w[i+1]。问安排怎样的合并顺序，能够使得总合并代价达到最小。

[link](http://wikioi.com/problem/1048/)

Solution explained: 

>sum[i[用于记录从第1堆到第i堆（包含i）石子的总重量。
>
>dp[i][j]表示从第i堆（包含i）到第j堆（包含j）石子的合并的最小代价。
>
>状态转移方程为：dp[i][j] = minimize{dp[i][k] + dp[k+1][j] + sum[j] - sum[i-1]}, k从i到j（不包含j）。
>
>len=2表示第一次合并的情况，此时合并的石子为2堆。此时，i从1到n-len+1，j=i+len-1。

Quoted from [this blog](http://blog.csdn.net/kingzone_2008/article/details/12361327) and the solution is well explained on [wikiio](http://wikioi.com/solution/list/1048/). 

### Type 4: Tree Dp

__Binary Tree Maximum Path Sum__

This is a difficult question, but I solved it. I feel happy. 

    private class ResultType {
        int maxPath;
        int depth;

        ResultType(int a, int b) {
            this.maxPath = a;
            this.depth = b;
        }
    }

    public int maxPathSum(TreeNode root) {
        if (root == null) {
            return 0;
        }
        return helper(root).maxPath;
    }

    private ResultType helper(TreeNode node) {
        if (node == null) {
            return new ResultType(Integer.MIN_VALUE, 0);
        }
        ResultType ll = helper(node.left);
        ResultType rr = helper(node.right);
        int maxPath = node.val + ll.depth + rr.depth;
        maxPath = Math.max(maxPath, ll.maxPath);
        maxPath = Math.max(maxPath, rr.maxPath);
        int depth = 0;
        depth = Math.max(depth, node.val + Math.max(ll.depth, rr.depth));
        return new ResultType(maxPath, depth);
    }

### Additional questions

__Maximum Subarray__

    public int maxSubArray(int[] A) {
        if (A == null || A.length == 0) {
            return 0;
        }
        int len = A.length;
        int[] dp = new int[len];
        dp[0] = A[0];
        for (int i = 1; i < len; i++) {
            dp[i] = A[i];
            if (dp[i - 1] > 0)
                dp[i] += dp[i - 1];
        }
        int max = Integer.MIN_VALUE;
        for (Integer i : dp)
            max = Math.max(max, i);
        return max;
    }
