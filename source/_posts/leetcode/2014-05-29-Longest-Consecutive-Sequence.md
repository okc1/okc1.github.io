---
layout: post
title: "[LeetCode 128] Longest Consecutive Sequence"
comments: true
category: Leetcode

---

### Question 
[link](https://oj.leetcode.com/problems/longest-consecutive-sequence/)

<div class="question-content">
            <p></p><p>
Given an unsorted array of integers, find the length of the longest consecutive elements sequence.
</p>
<p>
For example,<br>
Given <code>[100, 4, 200, 1, 3, 2]</code>,<br>
The longest consecutive elements sequence is <code>[1, 2, 3, 4]</code>. Return its length: <code>4</code>.
</p>
<p>
Your algorithm should run in O(<i>n</i>) complexity.
</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">just coding is easy</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__I did not solve this question__. We are going to make use of __HashSet__. 

Information on HashSet from [official document](http://docs.oracle.com/javase/7/docs/api/java/util/HashSet.html): 

> __java.util.HashSet__

> This class __implements the Set interface__, backed by a __hash table__ (actually a HashMap instance). It makes no guarantees as to the __iteration order__ of the set; in particular, it does not guarantee that the order will remain constant over time. This class permits the __null element__.

> This class offers __constant time performance__ for the basic operations (add, remove, contains and size), assuming the hash function disperses the elements properly among the buckets. Iterating over this set requires time proportional to the sum of the HashSet instance's size (the number of elements) plus the "capacity" of the backing HashMap instance (the number of buckets). Thus, it's very important not to set the initial capacity too high (or the load factor too low) if iteration performance is important.

> Note that this implementation is __not synchronized__. If multiple threads access a hash set concurrently, and at least one of the threads modifies the set, it must be synchronized externally. 

__To summarize it, HashSet__: 

1. implements Set interface

2. implemented by using a hash table

3. un-ordered

4. add, remove and contains methods have constant time O(1)

5. can have null element

6. not sync

### Solution

__Well explained in [this site](http://stackoverflow.com/a/7453295)__. 

> Dump everything to a hash set.

> Now go through the hashset. For each element, look up the set for all values neighboring the current value. Keep track of the largest sequence you can find, while removing the elements found from the set. Save the count for comparison.

> Repeat this until the hashset is empty.

> Assuming lookup, insertion and deletion are O(1) time, this algorithm would be O(N) time.

__Updated on July 4th, 2014__: Look at the 2nd for-loop. Here if I do 'for (Integer in: set)' to iterate all numbers, I will get "java.util.ConcurrentModificationException ". This is because we are iterating while modifying. __The most tricky part of this solution is iteration thru the array__, instead of the set. Take note of that! 

### Code

    public int longestConsecutive(int[] num) {
        int longest = 1;
        HashSet<Integer> set = new HashSet<Integer>();
        for (Integer in: num) set.add(in);
        for (Integer in: num) {
            int left = in - 1, right = in + 1;
            while (set.contains(left)) {
                set.remove(left);
                left --;
            }
            while (set.contains(right)) {
                set.remove(right);
                right ++;
            }
            longest = Math.max(longest, right - left - 1);
        }
        return longest;
    }
