---
layout: post
title: "[LeetCode 56] Merge Intervals"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/merge-intervals/)

<div class="question-content">
            <p></p><p>Given a collection of intervals, merge all overlapping intervals.</p>

<p>
For example,<br>
Given <code>[1,3],[2,6],[8,10],[15,18]</code>,<br>
return <code>[1,6],[8,10],[15,18]</code>.
</p><p></p>
          </div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">5</td>
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
		<td bgcolor="yellow">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Solution

__The idea of the solution is not difficult__. First, sort the entire collection list by start time. Secondly, merge it. 

__The real difficult part is how to sort the collection__. 

__We can of course do insertion sort__, or __binary insertion sort__. However, from [this article](http://www.brpreiss.com/books/opus5/html/page487.html):

> The straight insertion algorithm presented in the preceding section does a linear search to find the position in which to do the insertion. However, since the element is inserted into a sequence that is already sorted, we can use a binary search instead of a linear search. Whereas a linear search requires O(n) comparisons in the worst case, a binary search only requires O(logn) comparisons. Therefore, if the cost of a comparison is significant, the binary search may be preferred.

{% img middle /assets/images/merge_interval_binary_insertion_sort_algo.png %}

__And from__ [wikipedia](http://en.wikipedia.org/wiki/Insertion_sort#Variants):

> If the cost of comparisons exceeds the cost of swaps, as is the case for example with string keys stored by reference or with human interaction (such as choosing one of a pair displayed side-by-side), then using binary insertion sort may yield better performance. Binary insertion sort employs a binary search to determine the correct location to insert new elements, and therefore performs ⌈log2(n)⌉ comparisons in the worst case, which is O(n log n). The algorithm as a whole still has a running time of O(n^2) on average because of the series of swaps required for each insertion.

So insertion sort algorithm may not be the best choice for us! 

__A more popular solution is using Collection.sort function__. 

> java.util.Collections
>
>public static <T> void sort(List<T> list, Comparator<? super T> c)
>
>Parameters: c
>
>The comparator to determine the order of the list. A null value indicates that the elements' natural ordering should be used.

A new class that implements the Comparator interface is created, and inside there is compare(Interval, Interval) method. [Here](http://www.cnblogs.com/lautsie/p/3254191.html) is one example of such solution. 

__The third solution is same as the second, but only different__ in implementing the comparator object. Note the following code from [this blog](http://rleetcode.blogspot.sg/2014/01/merge-intervals-java.html): 

Comparator<Interval> intervalComperator = new Comparator<Interval>(){
        public int compare(Interval i1, Interval i2){
                Integer i1St=i1.start;
                Integer i2St=i2.start;
                return i1St.compareTo(i2St);
        }
};

Read 3 pieces of code below. 

### My code

insertion sort, then merge: 

    public ArrayList<Interval> merge(ArrayList<Interval> intervals) {
        ArrayList<Interval> ans = new ArrayList<Interval>();
        int len = intervals.size();
        if (len == 0) return ans;
        ans.add(intervals.get(0));
        if (len == 1) return ans;
        // now intervals length is >= then 2
        if (intervals.get(0).start < intervals.get(1).start)
            ans.add(intervals.get(1));
        else ans.add(0, intervals.get(1));
        for (int i = 2; i < len; i++) {
            int cur = intervals.get(i).start;
            // now find number cur from ans<list>
            int left = 0, right = ans.size() - 1;
            while (right - left > 1) {
                int mid = (left + right) / 2;
                if (ans.get(mid).start < cur) left = mid;
                else right = mid;
            }
            // insert cur between left and right, unless:
            if (left == 0 && cur < ans.get(0).start)
                ans.add(0, intervals.get(i));
            else if (right == ans.size() - 1
                    && cur > ans.get(ans.size() - 1).start)
                ans.add(intervals.get(i));
            else
                ans.add(right, intervals.get(i));
        }
        // now merge ans
        int k = 0;
        while (k < ans.size() - 1) {
            while (k < ans.size() - 1 && ans.get(k).end >= ans.get(k + 1).start) {
                ans.get(k).end = Math.max(ans.get(k).end, ans.get(k + 1).end);
                ans.remove(k + 1);
            }
            k++;
        }
        return ans;
    }

__Recommended solution__. Creating a new Comparator class 

	/**
	 * Definition for an interval.
	 * public class Interval {
	 *     int start;
	 *     int end;
	 *     Interval() { start = 0; end = 0; }
	 *     Interval(int s, int e) { start = s; end = e; }
	 * }
	 */
	public class Solution {
	    public List<Interval> merge(List<Interval> intervals) {
	        if (intervals == null || intervals.size() == 0) {
	            return intervals;
	        }
	        Collections.sort(intervals, new IntervalComparator());
	        int p = 0;
	        // if p is the last element of the list, we should stop merging
	        while (p < intervals.size() - 1) {
	            // merge p with the next interval, if possible
	            if (intervals.get(p).end >= intervals.get(p + 1).start) {
	                intervals.get(p).end = Math.max(intervals.get(p).end, intervals.get(p + 1).end);
	                intervals.remove(p + 1);
	            } else {
	                p++;
	            }
	        }
	        return intervals;
	    }
	    
	    class IntervalComparator implements Comparator<Interval> {
	        public int compare(Interval a, Interval b) {
	            return a.start - b.start;
	        }
	    }
	}

__Third solution__, different way of writing Comparator.

    public ArrayList<Interval> merge(ArrayList<Interval> intervals) {
        if (intervals == null || intervals.size() < 2)
            return intervals;
        ArrayList<Interval> result = new ArrayList<Interval>();

        Comparator<Interval> intervalComperator = new Comparator<Interval>() {
            public int compare(Interval i1, Interval i2) {
                Integer i1St = i1.start;
                Integer i2St = i2.start;
                return i1St.compareTo(i2St);

            }
        };
        Collections.sort(intervals, intervalComperator);

        Interval current = intervals.get(0);
        int i = 1;
        while (i < intervals.size()) {
            Interval currentToCompare = intervals.get(i);
            if (current.end < currentToCompare.start) {
                result.add(current);
                current = currentToCompare;
            } else
                current.end = Math.max(current.end, currentToCompare.end);
            i++;
        }
        result.add(current);
        return result;
    }
