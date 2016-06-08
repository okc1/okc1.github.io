---
layout: post
title: "[NineChap 8] High Frequency Questions"
comments: true
category: NineChap

---

## Number & Bit questions

1. __[Single Number]({% post_url /leetcode/2014-06-01-Single-Number %})__
1. __[Single Number II]({% post_url /leetcode/2014-06-01-Single-Number-II %})__
1. __[Single Number III]({% post_url /question/2014-06-28-Single-Number-III %})__
1. __[Single Number IV]({% post_url /question/2014-06-28-Single-Number-IV %})__
1. __[Majority Number]({% post_url /lintcode/2014-06-28-Majority-Number %})__
1. __[Majority Number II]({% post_url /lintcode/2014-06-28-Majority-Number-II %})__
1. __[Majority Number III]({% post_url /lintcode/2014-06-28-Majority-Number-III %})__

## Subarray questions

Always using the idea of 前缀和. 

1. __[Best Time to Buy and Sell Stock]({% post_url /leetcode/2014-05-28-Best-Time-to-Buy-and-Sell-Stock %})__ - 贪心法
1. __[Best Time to Buy and Sell Stock II]({% post_url /leetcode/2014-05-28-Best-Time-to-Buy-and-Sell-Stock-II %})__
1. __[Best Time to Buy and Sell Stock III]({% post_url /leetcode/2014-05-28-Best-Time-to-Buy-and-Sell-Stock-III %})__
1. __[Maximum Subarray]({% post_url /leetcode/2014-05-20-Maximum-Subarray %})__
1. __[Minimum Subarray ]({% post_url /lintcode/2014-06-28-Minimum-subarray %})__
1. __[Maximum Subarray II]({% post_url /lintcode/2014-06-28-Maximum-subarray-II %})__
1. __[Subarray with 0 Sum]({% post_url /question/2014-07-04-Subarray-with-0-Sum %})__
1. __[Subarray with Particular Sum]({% post_url /question/2014-07-04-Subarray-with-Particular-Sum %})__
1. __[Subarray with Sum Closest]({% post_url /question/2014-07-04-Subarray-with-Sum-Closest %})__

## N Sum questions

1. __[Two Sum]({% post_url /leetcode/2014-04-26-two-sum %})__ - difficult
1. __[3 Sum]({% post_url /leetcode/2014-05-02-3Sum %})__
1. __[3 Sum Closest]({% post_url /leetcode/2014-05-02-3Sum-Closest %})__
1. __[4 Sum]({% post_url /leetcode/2014-05-03-4Sum %})__ - doing a O(n^3) solution is good enough.
1. __k sum questions__ are basically solved with O(n^(k-1)) time. Faster solution is available but too complex. 

## L 家最爱

1. __[Pow(x,n)]({% post_url /leetcode/2014-05-15-PowXN %})__
1. __[Sqrt(x)]({% post_url /leetcode/2014-05-21-SqrtX %})__
1. __[Trailing Zeros of Factorial]({% post_url /lintcode/2014-07-02-Trailing-Zero-of-Factorial %})__
1. __[Check Power of 2]({% post_url /question/2014-07-04-Check-Power-of-2 %})__

## Additional questions

1. __[Partition Array]({% post_url /lintcode/2014-06-28-Partition-array %})__
1. __[Sort Color]({% post_url /leetcode/2014-05-21-Sort-Colors %})__

## Code

#### Number questions

__Single Number__

    public int singleNumber(int[] A) {
        int x = 0;
        for (Integer a: A) {
            x = x ^ a;
        }
        return x;
    }

__Single Number II__

Last time, I used an array of size 32 to store count, but it's actually not necessary. 

    public int singleNumber(int[] A) {
        int ans = 0;
        for (int i = 0; i < 32; i++) {
            int count = 0;
            for (Integer a: A) {
                count += ((a >> i) & 1);
            }
            ans |= (count % 3) << i;
        }
        return ans;
    }

#### Subarray questions

__Best Time to Buy and Sell Stock__

    public int maxProfit(int[] prices) {
        if (prices == null || prices.length == 0) {
            return 0;
        }
        int min = prices[0];
        int profit = 0;
        for (Integer p: prices) {
            min = Math.min(min, p);
            profit = Math.max(profit, p - min);
        }
        return profit;
    }

__Best Time to Buy and Sell Stock II__

    public int maxProfit(int[] prices) {
        if (prices == null || prices.length == 0) {
            return 0;
        }
        int pre = prices[0];
        int profit = 0;
        for (Integer p: prices) {
            if (p > pre) {
                profit += p - pre;
            }
            pre = p;
        }
        return profit;
    }

__Best Time to Buy and Sell Stock III__

It's important to note the 2nd last line of the code, where we consider the corner case of doing only 1 transaction. 

It's always best to list a simple test case and walk it thru before submitting the code. 

    public int maxProfit(int[] prices) {
        if (prices == null || prices.length == 0) {
            return 0;
        }
        int len = prices.length;
        int[] dpLeft = new int[len];
        int leftMin = prices[0];
        for (int i = 1; i < len; i++) {
            dpLeft[i] = Math.max(dpLeft[i - 1], prices[i] - leftMin);
            leftMin = Math.min(leftMin, prices[i]);
        }
        int[] dpRight = new int[len];
        int rightMax = prices[len - 1];
        for (int i = len - 2; i >= 0; i--) {
            dpRight[i] = Math.max(dpRight[i + 1], rightMax - prices[i]);
            rightMax = Math.max(rightMax, prices[i]);
        }
        // now iterate the 2 DP array and find out the largest possible profit
        int profit = 0;
        for (int i = 0; i < len - 1; i++) {
            profit = Math.max(profit, dpLeft[i] + dpRight[i + 1]);
        }
        int oneTransaction = Math.max(dpLeft[len - 1], dpRight[0]);
        return Math.max(profit, oneTransaction);
    }

__Maximum Subarray__

    public int maxSubArray(int[] A) {
        if (A == null || A.length == 0) {
            return 0;
        }
        int max = Integer.MIN_VALUE;
        int pre = 0;
        // the largest sum ending at previous position in the array
        for (Integer a: A) {
            max = Math.max(max, pre + a);
            pre = Math.max(0, pre + a);
        }
        return max;
    }

#### 3Sum questions

__Two Sum__

This solution is O(nlgn) time. 

Alternatively, we can use HashMap to solve this problem with O(n) time. 

    public int[] twoSum(int[] numbers, int target) {
        // write your code here
        int[] ans = new int[2];
        if (numbers == null || numbers.length == 0) {
            return ans;
        }
        int len = numbers.length;
        Pair[] pairs = new Pair[len];
        for (int i = 0; i < len; i++) {
            pairs[i] = new Pair(numbers[i], i + 1);
        }
        Arrays.sort(pairs);
        int left = 0;
        int right = len - 1;
        while (left < right) {
            if (pairs[left].num + pairs[right].num == target) {
                ans[0] = pairs[left].index;
                ans[1] = pairs[right].index;
                Arrays.sort(ans);
                break;
            } else if (pairs[left].num + pairs[right].num > target) {
                right--;
            } else {
                left++;
            }
        }
        return ans;
    }
	
    class Pair implements Comparable<Pair> {
        int num;
        int index;
        
        public Pair(int a, int b) {
            num = a;
            index = b;
        }
        
        public int compareTo(Pair another) {
            return this.num - another.num;
        }
    }

__3 Sum__

    public ArrayList<ArrayList<Integer>> threeSum(int[] numbers) {
        ArrayList<ArrayList<Integer>> ans = new ArrayList<ArrayList<Integer>>();
        if (numbers == null || numbers.length == 0) {
            return ans;
        }
        Arrays.sort(numbers);
        int len = numbers.length;
        for (int i = 0; i < len; i++) {
            if (i > 0 && numbers[i - 1] == numbers[i]) {
                continue;
            }
            int left = i + 1;
            int right = len - 1;
            // find 2 numbers that sums to - number[i]
            while (left < right) {
                int diff = numbers[left] + numbers[right] + numbers[i];
                if (diff == 0) {
                    ArrayList<Integer> triplet = new ArrayList<Integer>();
                    triplet.add(numbers[i]);
                    triplet.add(numbers[left]);
                    triplet.add(numbers[right]);
                    ans.add(triplet);
                }
                if (diff <= 0) {
                    left++;
                    while (left < len && numbers[left - 1] == numbers[left]) {
                        left++;
                    }
                }
                if (diff >= 0) {
                    right--;
                    while (right >= 0 && numbers[right + 1] == numbers[right]) {
                        right--;
                    }
                }
            }
        }
        return ans;
    }

__3 Sum Closest__

    public int threeSumClosest(int[] numbers, int target) {
        if (numbers == null || numbers.length == 0) {
            return 0;
        }
        Arrays.sort(numbers);
        int sum = 0;
        int diff = Integer.MAX_VALUE;
        int len = numbers.length;
        for (int i = 0; i < len; i++) {
            int left = i + 1;
            int right = len - 1;
            while (left < right) {
                int triple = numbers[left] + numbers[right] + numbers[i];
                if (triple == target) {
                    return target;
                } else if (triple < target) {
                    left++;
                } else {
                    right--;
                }
                if (Math.abs(target - triple) < diff) {
                    diff = Math.abs(target - triple);
                    sum = triple;
                }
            }
        }
        return sum;
    }

__4 Sum__

    public ArrayList<ArrayList<Integer>> fourSum(int[] numbers, int target) {
        ArrayList<ArrayList<Integer>> ans = new ArrayList<ArrayList<Integer>>();
        if (numbers == null || numbers.length == 0) {
            return ans;
        }
        Arrays.sort(numbers);
        int len = numbers.length;
        for (int i = 0; i < len - 3; i++) {
            if (i > 0 && numbers[i - 1] == numbers[i]) {
                continue;
            }
            for (int j = i + 1; j < len - 2; j++) {
                if (j > i + 1 && numbers[j - 1] == numbers[j]) {
                    continue;
                }
                int left = j + 1;
                int right = len - 1;
                while (left < right) {
                    int diff = numbers[left] + numbers[right] + numbers[i] + numbers[j] - target;
                    if (diff == 0) {
                        ArrayList<Integer> triplet = new ArrayList<Integer>();
                        triplet.add(numbers[i]);
                        triplet.add(numbers[j]);
                        triplet.add(numbers[left]);
                        triplet.add(numbers[right]);
                        ans.add(triplet);
                    }
                    if (diff <= 0) {
                        left++;
                        while (left < len && numbers[left - 1] == numbers[left]) {
                            left++;
                        }
                    }
                    if (diff >= 0) {
                        right--;
                        while (right >= 0 && numbers[right + 1] == numbers[right]) {
                            right--;
                        }
                    }
                }
            }
        }
        return ans;
    }

#### L 家最爱

__Pow(x,n)__

It's important to note that in Line 16, wrting 'while (pow * 2 <= y)' would not work (because of overflow). It took me a long time to find this bug. 

    public double pow(double x, int n) {
        if (n < 0) {
            return 1.0 / helper (x, 0 - n);
        } else {
            return helper(x, n);
        }
    }
    
    private double helper(double x, int y) {
        if (y == 0) {
            return 1.0;
        }
        int pow = 1;
        double num = x;
        while (pow <= y / 2) {
            num *= num;
            pow <<= 1;
        }
        return num * helper(x, y - pow);
    }

__Sqrt(x)__

Note that in Line 8, we must declare left and right as 'long', not 'int', otherwise there will be overflow problems. It took me a long time to find this bug. 

    public int sqrt(int x) {
        if (x < 0) {
            return -1;
        } else if (x < 2) {
            return x;
        }
        long left = 1;
        long right = x;
        while (left + 1 < right) {
            long mid = left + (right - left) / 2;
            if (mid * mid < x) {
                left = mid;
            } else if (mid * mid > x) {
                right = mid;
            } else {
                return (int) mid;
            }
        }
        return (int) left;
    }

#### Additional

__Sort Color__

    public void sortColors(int[] A) {
        if (A == null || A.length == 0) {
			return;
		}
		int len = A.length;
		partition(A, 0, len - 1, 0);
		int p = 0;
		while (p < len && A[p] == 0) {
			p++;
		}
		partition(A, p, len - 1, 1);
    }
	
	private void partition(int[] A, int start, int end, int target) {
		// find the target and put it on the left side of the array
		while (start < end) {
			while (start < A.length && A[start] == target) {
				start++;
			}
			while (end >= 0 && A[end] != target) {
				end--;
			}
			if (start > end) {
				break;
			} else {
				int temp = A[start];
				A[start] = A[end];
				A[end] = temp;
			}
		}
	}
