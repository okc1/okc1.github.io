---
layout: post
title: "[LeetCode 77] Combinations"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/combinations/)

<div class="question-content">
            <p></p><p>
Given two integers <i>n</i> and <i>k</i>, return all possible combinations of <i>k</i> numbers out of 1 ... <i>n</i>.
</p>
<p>
For example,<br>
If <i>n</i> = 4 and <i>k</i> = 2, a solution is:
</p>

<pre>[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
</pre><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a very classic problem__. 

The solution is standard, and we must be able to write it without even using our __brain__ (only use hands). 

### Solution

Solution 1, recursive DFS calls. 

Solution 2, nested loop. Code is shown below. 

### Code

__First, my DFS solution__


    public ArrayList<ArrayList<Integer>> combine(int n, int k) {
        ArrayList<ArrayList<Integer>> ans = new ArrayList<ArrayList<Integer>>();
        if (k == 0) return ans;
        helper(ans, new ArrayList<Integer>(), n, k, 0, 0);
        return ans;
    }

    private void helper(ArrayList<ArrayList<Integer>> ans,ArrayList<Integer> list,
                        int n, int k, int curPt, int preNum) {
        if (curPt == k) {
            ans.add(new ArrayList<Integer>(list));
            return;
        }
        for (int i = preNum + 1; i <= n - k + 1 + curPt; i ++) {
            list.add(i);
            helper(ans, list, n, k, curPt + 1, i);
            list.remove(list.size() - 1);
        }
    }


__Second, my nested for-loop solution__


    public ArrayList<ArrayList<Integer>> combine(int n, int k) {
        ArrayList<ArrayList<Integer>> ans = new ArrayList<ArrayList<Integer>>();
        ans.add(new ArrayList<Integer>());
        if (n == 0 || k == 0 || k > n) return ans;
        ArrayList<ArrayList<Integer>> temp = null;
        for (int i = 0; i < k; i ++) {
            temp = new ArrayList<ArrayList<Integer>>();
            for (ArrayList<Integer> a: ans) {
                for (int j = 1; j <= n; j ++) {
                    if (a.size() > 0 && a.get(a.size() - 1) >= j) 
                        continue;
                    a.add(j);
                    temp.add(new ArrayList<Integer>(a));
                    a.remove(a.size() - 1);
                }
            }
            ans = temp;
        }
        return ans;
    }

__Updated June 14th, rewrote the code using template__

    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> ans = new LinkedList<List<Integer>>();
        if (n == 0 || k == 0 || n < k) {
            return ans;
        }
        helper(ans, new LinkedList<Integer>(), n, k, 1);
        return ans;
    }
    
    private void helper(List<List<Integer>> ans, List<Integer> path, int n, int k, int pos) {
        if (path.size() == k) {
            ans.add(new LinkedList<Integer>(path));
            return;
        }
        for (int i = pos; i <= n; i++) {
            path.add(i);
            helper(ans, path, n, k, i + 1);
            path.remove(path.size() - 1);
        }
    }
