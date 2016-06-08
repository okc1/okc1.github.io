---
layout: post
title: "[LintCode] Recover Rotated Sorted Array"
comments: true
category: Lintcode
tags: [ ]
---

### Question 

[link](http://www.lintcode.com/en/problem/recover-rotated-sorted-array/)

<div style="min-height:100px" class="bg-color bg-img font-color">

    <p class="font-color">
        Given a <strong>rotated</strong> sorted array, recover it to sorted array in-place.
    </p>
    <div class="m-t-lg m-b-lg bg-color bg-img font-color">
        <b>Example</b>
        <div class="bg-color bg-img font-color">
            <p class="font-color"><span style="color:#B22222;" class="font-color"><strong>[4, 5, 1, 2, 3]</strong></span> -&gt; <span style="color:#B22222;" class="font-color"><strong>[1, 2, 3, 4, 5]</strong></span>
            </p>
        </div>
    </div>

    <div>
        <b>Challenge</b>
        <div>
            <p class="font-color">
                In-place, O(1) extra space and O(n) time.
            </p>
        </div>
    </div>

    <div class="m-t-lg m-b-lg bg-color bg-img font-color">
        <b>Clarification</b>
        <div id="clarification" class=" bg-color bg-img font-color">
            <p class="font-color">What is rotated array:</p>

            <p class="font-color">&nbsp; &nbsp; - For example, the orginal array is [1,2,3,4], The rotated array of it can be [1,2,3,4], [2,3,4,1], [3,4,1,2], [4,1,2,3]</p>

        </div>
    </div>
</div>

### Analysis

O(n) time and O(a) space is required. 

Find the rotate position and rotate each half. After this: 

<p class="font-color"><span style="color:#B22222;" class="font-color"><strong>[4, 5, 1, 2, 3]</strong></span> -&gt; <span style="color:#B22222;" class="font-color"><strong>[5, 4, 3, 2, 1]</strong></span>
</p>

Then reverse it again. This solution is called "三步翻转法", an extremely common interview algorithm. Similar questions are [[LeetCode 151] Reverse Words in a String]({% post_url /leetcode/2014-06-03-Reverse-Words-in-a-String %}). 

__Updated on Apr 11th, 2015__: 

Thanks to the __nice little help from [Shawn](https://disqus.com/by/disqus_QOTDaDZFgi/)__, I found out that using __binary search__ to find the rotation point is impossible, because of duplication. I wasn't able to point this out previously, thus apologize to all!

### My code 

	public void recoverRotatedSortedArray(ArrayList<Integer> nums) {
		// write your code
		if (nums == null || nums.size() <= 1) {
			return;
		}
		int p = 1;
		while (p < nums.size()) {
			if (nums.get(p - 1) > nums.get(p)) {
				break;
			}
			p++;
		}
		inPlaceRotate(nums, 0, p - 1);
		inPlaceRotate(nums, p, nums.size() - 1);
		inPlaceRotate(nums, 0, nums.size() - 1);
	}

	private void inPlaceRotate(ArrayList<Integer> nums, int left, int right) {
		while (left < right) {
			int temp = nums.get(left);
			nums.set(left, nums.get(right));
			nums.set(right, temp);
			left++;
			right--;
		}
	}
