---
layout: post
title: "[NineChap 7] Data Structure"
comments: true
category: NineChap

---

## Data Structure

Data structure is a way to manage data. It provides some methods to handle data stream. For example, DB is a DS.

### Stack and Queue

1. __[Min-stack]({% post_url /question/2014-07-01-Min-Stack %})__

1. __[Implement a queue by two stacks]({% post_url /question/2014-07-01-Implement-queue-with-stack %})__

1. __[Largest Rectangle in histogram]({% post_url /leetcode/2014-05-23-Largest-Rectangle-in-Histogram %})__

### Hash

#### Hash function

1. MD5
1. Magic number 33 (__PHP hash function [DJBX33A](http://events.ccc.de/congress/2011/Fahrplan/attachments/2007_28C3_Effective_DoS_on_web_application_platforms.pdf)__)

Magic Number: 

    int hashfunc(String key) {
        int sum = 0;
        for (int i = 0; i < key.length(); i++) {
            sum = sum * 33 + (int)(key.charAt(i));
            sum = sum % HASH_TABLE_SIZE;
        }
        return sum
    }
    
#### Collision

1. __Close hashing (also called Open addressing)__

    Resolves conflict by probing, or searching through alternate locations in the array
        
    Suck scheme may cause the lookup cost to skyrocket. Not good to use.

1. __Open hashing__

    Keys stored in linked lists attached to cells of the hash table.
    
    Practically, hash size set around 10 times the size of data
    
    Used by Java and most other languages. 

#### Rehashing

1. Memcached is a general-purpose distributed memory caching system. One of its bottleneck is rehashing, which locks down the entire hash.

1. Dynamic resizing (normally size * 2) and copy all elements into the new hash. 

1. Extremely slow process, we should try to avoid it by setting a large enough initial size. 

#### Hash questions:

1. __[Implement a hashmap]({% post_url /question/2014-07-01-Implement-Hashmap %})__

1. __[HashMap vs Hashtable vs HashSet]({% post_url /design/2014-07-01-Hashmap-Hashtable-Hashset %})__

1. __[LRU Cache]({% post_url /leetcode/2014-06-03-LRU-Cache %})__

1. __[Longest consecutive sequence]({% post_url /leetcode/2014-05-29-Longest-Consecutive-Sequence %})__

### Heap

1. Child is always larger than parent
1. Heap is not a sorted structure, but it's partially ordered
1. Heap is always balanced 

Heap is better than array because average of 3 operations is O(logn), but array is O(n). 

>Add O(log N)
>
>Remove O(log N)
>
>Min/Max O(1)

#### Heap implementation: 

1. Low Level: dynamic array, not list

1. Internal Method: Shiftup, Shiftdown operations

1. A heap is a complete binary tree (最优二叉树) __represented by an array__

1. When removing element from heap, we actually uses HashMap to find that element.

> Heaps are usually implemented in an array, and do not require pointers between elements.
>
> Full and almost full binary heaps may be represented in a very space-efficient way using an array alone. The first element will contain the root. The next two elements of the array contain its children. The next four contain the four children of the two child nodes, etc. 
>
> Thus the children of the node at position n would be at positions 2n+1 and 2n+2. 

So to summarize: 

1. elems[1] - root, also the minimum elem in elems.
1. elems[i]: left child is elems[i*2], right child is elems[i*2+1]

Implementation code: 

    Add:
        Push back to elems; size ++; Siftup;
    Remove:
        Replace the elem to be removed with the last elem; 
        size --; 
        Siftup and Siftdown.

#### Heap questions:

1. __[Median in a stream of integers]({% post_url /question/2014-07-01-Median-in-stream-of-integers %})__

1. __[The Skyline Problem]({% post_url /question/2014-07-01-The-Skyline-Problem %})__

### Interval Tree

Easily find the max/min value in an interval. 2 example questions are: 

1. Find min/max/sum in an interval
1. 最长的连续1

## Code

__Largest Rectangle in histogram__

    public int largestRectangleArea(int[] height) {
        if (height == null || height.length == 0) {
            return 0;
        }
        Stack<Integer> stack = new Stack<Integer>();
        stack.add(0);
        int len = height.length;
        int area = 0;
        for (int i = 1; i <= len; i++) {
            int h = i == len ? 0 : height[i];
            // pop a element and calculate its max area
            // pop until the top element is smaller than h, then push h
            while (!stack.isEmpty() && h < height[stack.peek()]) {
                int pos = stack.pop();
                int width = stack.isEmpty() ? i : i - stack.peek() - 1;
                area = Math.max(area, height[pos] * width);
            }
            stack.push(i);
        }
        return area;
    }

__LRU Cache__

I posted code in the new post. 

__Longest consecutive sequence__

    public int longestConsecutive(int[] num) {
        if (num == null || num.length == 0) {
            return 0;
        }
        HashSet<Integer> set = new HashSet<Integer>();
        for (Integer i: num) {
            set.add(i);
        }
        int longest = 0;
        for (Integer i: num) {
            if (!set.contains(i)) {
                continue;
            }
            int left = i - 1;
            while (set.contains(left)) {
                set.remove(left--);
            }
            int right = i + 1;
            while (set.contains(right)) {
                set.remove(right++);
            }
            longest = Math.max(longest, right - left - 1);
            set.remove(i);
        }
        return longest;
    }
