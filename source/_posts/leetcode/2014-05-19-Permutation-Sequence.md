---
layout: post
title: "[LeetCode 60] Permutation Sequence"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/permutation-sequence/)

<div class="question-content">
            <p></p><p>The set <code>[1,2,3,…,<i>n</i>]</code> contains a total of <i>n</i>! unique permutations.</p>

<p>By listing and labeling all of the permutations in order,<br>
We get the following sequence (ie, for <i>n</i> = 3):
</p><ol>
<li><code>"123"</code></li>
<li><code>"132"</code></li>
<li><code>"213"</code></li>
<li><code>"231"</code></li>
<li><code>"312"</code></li>
<li><code>"321"</code></li>
</ol>
<p></p>

<p>Given <i>n</i> and <i>k</i>, return the <i>k</i><sup>th</sup> permutation sequence.</p>

<p><b>Note:</b> Given <i>n</i> will be between 1 and 9 inclusive.</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a math problem__. Trying to solve it using __DFS__ like in "Permutation" or "N queen" will get time limit exceed exception.

[This blog](http://fisherlei.blogspot.sg/2013/04/leetcode-permutation-sequence-solution.html) have a very good explanation of the math solution. 

<blockquote cite="http://fisherlei.blogspot.sg/2013/04/leetcode-permutation-sequence-solution.html">
    <div>
        <br>[Thoughts]
        <br>两个解法。
        <br>第一，DFS
        <br>递归遍历所有可能，然后累加计算，直至到K为止。
        <br>
        <br>第二，数学解法。
        <br>
        <br>假设有n个元素，第K个permutation是
        <br>a1, a2, a3, ..... &nbsp; ..., an
        <br>那么a1是哪一个数字呢？
        <br>
        <br>那么这里，我们把a1去掉，那么剩下的permutation为
        <br>a2, a3, .... .... an, 共计n-1个元素。 n-1个元素共有(n-1)!组排列，那么这里就可以知道
        <br>
        <br>设变量K1 = K
        <br>a1 = K1 / (n-1)!
        <br>
        <br>同理，a2的值可以推导为
        <br>a2 = K2 / (n-2)!
        <br>K2 = K1 % (n-1)!
        <br>&nbsp;.......
        <br>a(n-1) = K(n-1) / 1!
        <br>K(n-1) = K(n-2) /2!
        <br>
        <br>an = K(n-1)
    </div>
</blockquote>

### Solution

__I have written a math recursive solution__ and code is below. It's very straight-forward. 

There is also __direct math solution__. However, how to handle the removal of elements from the unmatched list is a tough problem. __I saw a lot of people using swap to do it__, but I don't like this idea because of the bad readability of code. 

__Finally I found a readable code from [this blog](http://xiaochongzhang.me/blog/?p=693)__. It's a very good solution. 

### My code

__updated on my birthday this year__

    public String getPermutation(int n, int k) {
        int index = k - 1;
        List<Integer> nums = new ArrayList<Integer>();
        for (int i = 1; i <= n; i++) {
            nums.add(i);
        }
        String ans = "";
        for (int i = n - 1; i >= 1; i--) {
            int fact = factorial(i);
            int nextIndex = index / fact;
            index = index % fact;
            ans += nums.remove(nextIndex);
        }
        ans += nums.get(0);
        return ans;
    }
    
    private int factorial(int x) {
        if (x == 0) return 0;
        int ans = 1;
        for (int i = 2; i <= x; i++) {
            ans *= i;
        }
        return ans;
    }
