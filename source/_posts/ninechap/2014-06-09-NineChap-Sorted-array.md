---
layout: post
title: "[NineChap 2.2] Sorted Array"
comments: true
category: NineChap

---

## Sorted Array 


#### Template

There is no template. 

#### Question list

1. __[Remove Duplicates from Sorted Array]({% post_url /leetcode/2014-05-09-Remove-Duplicates-from-Sorted-Array %})__

2. __[Remove Duplicates from Sorted Array II]({% post_url /leetcode/2014-05-22-Remove-Duplicates-from-Sorted-Array-II %})__

3. __[Merge Sorted Array]({% post_url /leetcode/2014-05-23-Merge-Sorted-Array %})__

4. __[Median of Two Sorted Arrays]({% post_url /leetcode/2014-04-26-Median-of-Two-Sorted-Arrays %})__

5. __[Recover Rotated Sorted Array]({% post_url /lintcode/2014-06-08-Recover-Rotated-Sorted-Array %})__

#### Additional

1. __[Reverse Words in a String]({% post_url /leetcode/2014-06-03-Reverse-Words-in-a-String %})__

2. __Rotate String__

    Given string "abcdefg" and offset = 3, the rotated string is "efgabcd". 

## Code

__Remove Duplicates from Sorted Array__ 

    public int removeDuplicates(int[] A) {
        if (A == null || A.length == 0) {
			return 0;
		}
		int left = 1;
		int right = 1;
		while (right < A.length) {
			if (A[right - 1] != A[right]) {
				A[left] = A[right];
				left++;
			}
			right++;
		}
		return left;
    }

__Remove Duplicates from Sorted Array II__ - slightly difficult in coding

    public int removeDuplicates(int[] A) {
        if (A == null || A.length == 0) {
			return 0;
		}
		int left = 1;
		int right = 1;
		boolean twice = false;
		while (right < A.length) {
			if (A[right - 1] != A[right]) {
				A[left++] = A[right++];
				twice = false;
			} else if (!twice){
				A[left++] = A[right++];
				twice = true;
			} else {
				right++;
			}
		}
		return left;
    }

__Merge Sorted Array__

Easy question, tail to head merge. 

__Median of Two Sorted Arrays__

This question is Find kth largest from A&B. Refer to original post. 

__Recover Rotated Sorted Array__

I wrote a new post. 

__Reverse Words in a String__

    public String reverseWords(String s) {
		if (s == null || s.length() == 0) {
			return s;
		}
		String[] words = s.split(" ");
		String firstReversed = "";
		for (int i = 0; i < words.length; i ++) {
		    if (words[i].equals("")) continue;
			firstReversed += inPlaceReverse(words[i]) + " ";
		}
		return inPlaceReverse(firstReversed);
    }
	
	private String inPlaceReverse(String str) {
		if (str == null || str.length() == 0) return str;
		char[] chars = str.trim().toCharArray();
		int left = 0;
		int right = chars.length - 1;
		while (left < right) {
			char temp = chars[left];
			chars[left] = chars[right];
			chars[right] = temp;
			left ++;
			right --;
		}
		return String.valueOf(chars);
	}

__Rotate String__

Same strategy. 

## Conclusion

1. If array is sorted, try binary search
2. If array is not sorted, try sort it first
3. When you see 'rotated array', think of 'list reverse'.
