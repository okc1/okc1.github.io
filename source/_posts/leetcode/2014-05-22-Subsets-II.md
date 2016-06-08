---
layout: post
title: "[LeetCode 90] Subsets II"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/subsets-ii/)

<div class="question-content">
            <p></p><p>
Given a collection of integers that might contain duplicates, <i>S</i>, return all possible subsets.
</p>
<p><b>Note:</b><br>
</p><ul>
<li>Elements in a subset must be in non-descending order.</li>
<li>The solution set must not contain duplicate subsets.</li>
</ul>
<p></p>
<p>
For example,<br>
If <b><i>S</i></b> = <code>[1,2,2]</code>, a solution is:
</p>

<pre>[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
</pre><p></p>
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
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a question based on "Subsets" question__. 

Solution is similar, only need to add features to avoid duplication. 

### Solution

Based on the solution of previous question, I only add 1 variable called __nonDupSize__, which is the size that I need to merge new element with. For example, __input = {1, 2, 3, 3}__

> Initialize the subset:  {}

> Added element "1": {}, __{"1"}__ (1 more elements)

> Added element "2": {}, {"1"}, __{"2"}, {"1", "2"}__ (2 more elements)

> Added element "3": {}, {"1"}, {"2"}, {"1", "2"}, __{"3"}, {"1","3"}, {"2","3"}, {"1", "2","3"}__ (4 more elements)

> Added element "3": {}, {"1"}, {"2"}, {"1", "2"}, {"3"}, {"1","3"}, {"2","3"}, {"1","2","3"}, __{"3","3"}, {"1","3","3"}, {"2","3","3"}, {"1","2","3","3"}__ (4 more elements)

So instead of getting every list and merge with new element, I only get the lists of pre-calculated size (from bottom), and merge. Someone is having [similar solution](http://blog.csdn.net/perfect8886/article/details/22922785) using a start-pointer.

### Code

__my code__

    public ArrayList<ArrayList<Integer>> subsetsWithDup(int[] num) {
        ArrayList<ArrayList<Integer>> ans = new ArrayList<ArrayList<Integer>>();
        ans.add(new ArrayList<Integer>());
        Arrays.sort(num);
        // In this solution I introduce a new variable: nonDupSize
        int curSize = 1, nonDupSize = 1;
        for (int i = 0; i < num.length; i ++) {
            curSize = ans.size();
            if (i > 0 && num[i] != num[i - 1]) nonDupSize = curSize;
            for (int j = curSize - nonDupSize; j < curSize; j ++) {
                ArrayList<Integer> cur = new ArrayList<Integer>(ans.get(j));
                cur.add(num[i]);
                ans.add(cur);
            }
        }
        return ans;
    }

__Updated on June 12th__ - solution using the 'Permutation Model'. 

    public List<List<Integer>> subsetsWithDup(int[] num) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        if(num == null || num.length == 0) {
            return result;
        }
        Arrays.sort(num);
        helper(result, new LinkedList<Integer>(), num, 0);
        return result;
    }
    
    private void helper(List<List<Integer>> ans, List<Integer> path, int[] num, int position) {
        ans.add(new LinkedList<Integer>(path));
        for (int i = position; i < num.length; i ++) {
            if (i > position && num[i - 1] == num[i]) {
                // if duplicate, only append num[position]
                continue;
            }
            path.add(num[i]);
            helper(ans, path, num, i + 1);
            path.remove(path.size() - 1);
        }
    }
