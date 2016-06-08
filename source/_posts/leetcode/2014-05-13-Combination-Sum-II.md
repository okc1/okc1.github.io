---
layout: post
title: "[LeetCode 40] Combination Sum II"
comments: true
category: Leetcode

---


### Question 
[link](http://oj.leetcode.com/problems/combination-sum-ii/)

<div class="question-content">
            <p></p><p>
Given a collection of candidate numbers (<b><i>C</i></b>) and a target number (<b><i>T</i></b>), find all unique combinations in <b><i>C</i></b> where the candidate numbers sums to <b><i>T</i></b>.
</p>

<p>Each number in <b><i>C</i></b> may only be used <b>once</b> in the combination.
</p>
<p><b>Note:</b><br>
</p><ul>
<li>All numbers (including target) will be positive integers.</li>
<li>Elements in a combination (<i>a</i><sub>1</sub>, <i>a</i><sub>2</sub>, … , <i>a</i><sub>k</sub>) must be in non-descending order. (ie, <i>a</i><sub>1</sub> ≤ <i>a</i><sub>2</sub> ≤ … ≤ <i>a</i><sub>k</sub>).</li>
<li>The solution set must not contain duplicate combinations.</li>
</ul>
<p></p>

<p>
For example, given candidate set <code>10,1,2,7,6,1,5</code> and target <code>8</code>, <br>
A solution set is: <br>
<code>[1, 7]</code> <br>
<code>[1, 2, 5]</code> <br>
<code>[2, 6]</code> <br>
<code>[1, 1, 6]</code> <br>
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
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This problem is derived from the "Combination Sum" problem__. 

The solution is the "Combination Sum" solution plus some duplication avoidance technique. 

### Solution

__Main part of this solution is same as "Combination Sum"__. There is only 2 lines of code that needs to be added/modified. 

__First change__, When go into the next recursive call, instead of: 

    helper(ans, cand, path, i, len, target - cand[i]);

Change it to 

    helper(ans, cand, path, i + 1, len, target - cand[i]);

__Second change__, inside the for-loop, instead of getting next element right away, we get the element with different value. The additional code is: 

    if (i > pos && candidates[i] == candidates[i - 1]) {
        continue;
    }

### My code 

    public class Solution {
        public List<List<Integer>> combinationSum2(int[] candidates, int target) {
            List<List<Integer>> ans = new ArrayList<List<Integer>>();
            if (candidates == null || candidates.length == 0) {
                return ans;
            }
            Arrays.sort(candidates);
            int len = candidates.length;
            helper(ans, candidates, new ArrayList<Integer>(), 0, len, target);
            return ans;
        }

        private void helper(List<List<Integer>> ans, int[] cand, List<Integer> path, int pos, int len, int target) {
            if (target == 0) {
                ans.add(new ArrayList<Integer>(path));
                return;
            } else if (target < 0) {
                return;
            }
            for (int i = pos; i < len; i++) {
                // if 'i' points to a repeated number, skip.
                if (i > pos && cand[i] == cand[i - 1]) {
                    continue;
                }
                // insert cand[i] into path list, and continue search dfs
                path.add(cand[i]);
                helper(ans, cand, path, i + 1, len, target - cand[i]);
                path.remove(path.size() - 1);
            }
        }
    }
