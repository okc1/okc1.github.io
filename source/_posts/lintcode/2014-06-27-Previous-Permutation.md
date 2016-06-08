---
layout: post
title: "[LintCode] Previous Permutation"
description: ""
category: LintCode

---

### Question 

[link](http://www.lintcode.com/en/problem/previous-permuation/)

<div style="min-height:100px">
<p>Given a list of integers, which denote a permutation.</p>

<p>Find the previous permutation in ascending order.</p>
    
<div class="m-t-lg m-b-lg">
      <b>Note</b>
      <div><p>The list may contains duplicate integers.</p>
      </div>
</div>
    
<div class="m-t-lg m-b-lg">
      <b>Example</b>
      <div><p>For <strong><span style="color:#B22222;">[1,3,2,3]</span></strong>, the previous permutation is <span style="color:#B22222;"><strong>[1,2,3,3]</strong></span></p>

<p>For <span style="color:#B22222;"><strong>[1,2,3,4]</strong></span>, the previous permutation is <span style="color:#B22222;"><strong>[4,3,2,1]</strong></span></p>
    </div>
</div>
</div>

### Analysis 

This is almost the same question as "Next Permutation". 

1. Find
1. Swap
1. Replace

### Code

    public ArrayList<Integer> previousPermuation(ArrayList<Integer> nums) {
		// write your code
		if (nums == null || nums.size() == 0) {
		    return null;
		}
		int len = nums.size();
		int p = len - 2;
		// 1. find 1st increasing position from the back
		while (p >= 0 && nums.get(p) <= nums.get(p + 1)) {
		    p--;
		}
		// 2. swap p with the first smaller value from the back
		if (p != -1) {
		    int q = len - 1;
		    while (nums.get(q) >= nums.get(p)) {
		        q--;
		    }
		    swap(nums, p, q);
		}
		// swap array in range of (p+1, end)
		int left = p + 1;
		int right = len - 1;
		while (left < right) {
		    swap(nums, left++, right--);
		}
		return nums;
    }
    
    private void swap(ArrayList<Integer> num, int p, int q) {
        int temp = num.get(p);
	    num.set(p, num.get(q));
	    num.set(q, temp);
    }
