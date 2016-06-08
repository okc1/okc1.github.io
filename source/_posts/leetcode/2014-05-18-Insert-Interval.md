---
layout: post
title: "[LeetCode 57] Insert Interval"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/insert-interval/)

<div class="question-content">
            <p></p><p>Given a set of <i>non-overlapping</i> intervals, insert a new interval into the intervals (merge if necessary).</p>

<p>You may assume that the intervals were initially sorted according to their start times.</p>

<p>
<b>Example 1:</b><br>
Given intervals <code>[1,3],[6,9]</code>, insert and merge <code>[2,5]</code> in as <code>[1,5],[6,9]</code>.
</p>

<p>
<b>Example 2:</b><br>
Given <code>[1,2],[3,5],[6,7],[8,10],[12,16]</code>, insert and merge <code>[4,9]</code> in as <code>[1,2],[3,10],[12,16]</code>.
</p>

<p>
This is because the new interval <code>[4,9]</code> overlaps with <code>[3,5],[6,7],[8,10]</code>.
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
		<td bgcolor="yellow">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Solution

__This is not an easy question, though it's similar to the question "Merge Intervals"__. 

First code is my solution. 

__Second code is from [this repo](https://github.com/yuanx/leetcode/blob/master/InsertInterval.java)__. This is only 1 iteration, but in 3 stages. First, add all intervals ahead of newInterval into ans. Second, merge anything that can be merged with newInterval, and add to ans. Third, add the rest of intervals into ans. 

__Third code is from [this blog](http://www.programcreek.com/2012/12/leetcode-insert-interval/)__. It's a very tricky solution. 

### My code

__My code__

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
	    public List<Interval> insert(List<Interval> intervals, Interval newInterval) {
	        if (intervals == null) {
	            return null;
	        }
	        int p = 0;
	        while (p < intervals.size() && intervals.get(p).start < newInterval.start) {
	            p++;
	        }
	        intervals.add(p, newInterval);
	        if (p > 0) {
	            p--;
	        }
	        // start merging from (p)th element
	        while (p < intervals.size() - 1) {
	            if (intervals.get(p).end >= intervals.get(p + 1).start) {
	                intervals.get(p).end = Math.max(intervals.get(p).end, intervals.get(p + 1).end);
	                intervals.remove(p + 1);
	            } else {
	                p++;
	            }
	        }
	        return intervals;
	    }
	}

__Second code__. 

    public ArrayList<Interval> insert(ArrayList<Interval> intervals, Interval newInterval) {
        ArrayList<Interval> re = new ArrayList<Interval>();
        int len = intervals.size();
        int i = 0;
        while (i < len) {
            Interval temp = intervals.get(i);
            if (temp.end < newInterval.start)
                re.add(temp);
            else if (temp.start > newInterval.end)
                break;
            else {
                newInterval.start = Math.min(temp.start, newInterval.start);
                newInterval.end = Math.max(temp.end, newInterval.end);
            }
            i++;
        }
        re.add(newInterval);
        while (i < len) {
            re.add(intervals.get(i));
            i++;
        }
        return re;
    }

__Third code, a popular solution__. Very tricky and concise.

    public ArrayList<Interval> insert(ArrayList<Interval> intervals, Interval newInterval) {
        ArrayList<Interval> result = new ArrayList<Interval>();
        for(Interval interval: intervals){
            if(interval.end < newInterval.start){
                result.add(interval);
            }else if(interval.start > newInterval.end){
                result.add(newInterval);
                newInterval = interval;        
            }else if(interval.end >= newInterval.start 
                    || interval.start <= newInterval.end){
                newInterval = new Interval(
                    Math.min(interval.start, newInterval.start), 
                    Math.max(newInterval.end, interval.end));
            }
        }
        result.add(newInterval); 
        return result;
    }
