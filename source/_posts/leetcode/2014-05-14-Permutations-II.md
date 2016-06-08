---
layout: post
title: "[LeetCode 47] Permutations II"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/permutations-ii/)

<div class="question-content">
            <p></p><p>
Given a collection of numbers that might contain duplicates, return all possible unique permutations.
</p>

<p>
For example,<br>
<code>[1,1,2]</code> have the following unique permutations:<br>
<code>[1,1,2]</code>, <code>[1,2,1]</code>, and <code>[2,1,1]</code>.
</p><p></p>
          </div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="lime">2</td>
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

__This question is based on "Permutations"__, plus duplication avoidance. 

This question, together with "Permutations", is very classic and frequent questions, thus the basis for many similar DFS problems. Read [this blog](http://www.programcreek.com/2013/02/leetcode-permutations-ii-java/) for more. 

The idea is when getting element from remaining list and add to current list, check for duplication. __If the number occured before, skip operation__. (Don't forget sorting is required at first). 

The key points to keep in mind: 

1. Use another array to flag the 'visited' items
2. Check items with same value, and __ONLY USE THE FIRST INSTANCE OF THE SAME VALUE__. Which is to say, if current = previous, but previous is not visited, do not use current number. 

### My code 

	public class Solution {
	    public List<List<Integer>> permuteUnique(int[] num) {
	        List<List<Integer>> ans = new ArrayList<List<Integer>>();
	        if (num == null || num.length == 0) {
	            return ans;
	        }
	        int len = num.length;
	        Arrays.sort(num);
	        helper(ans, new ArrayList<Integer>(), num, len, new boolean[len]);
	        return ans;
	    }
	    
	    private void helper(List<List<Integer>> ans, List<Integer> path, int[] num, int len, boolean[] visited) {
	        if (path.size() == len) {
	            ans.add(new ArrayList<Integer>(path));
	            return;
	        }
	        for (int i = 0; i < len; i++) {
	            if (i > 0 && num[i - 1] == num[i] && !visited[i - 1]) {
	                // important: if previous number have same value as (i)th
	                // but have never been visited, then skip current number
	                continue;
	            }
	            if (!visited[i]) {
	                path.add(num[i]);
	                visited[i] = true;
	                helper(ans, path, num, len, visited);
	                path.remove(path.size() - 1);
	                visited[i] = false;
	            }
	        }
	    }
	}
