---
layout: post
title: "[LeetCode 46] Permutations"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/permutations/)

<div class="question-content">
            <p></p><p>
Given a collection of numbers, return all possible permutations.
</p>

<p>
For example,<br>
<code>[1,2,3]</code> have the following permutations:<br>
<code>[1,2,3]</code>, <code>[1,3,2]</code>, <code>[2,1,3]</code>, <code>[2,3,1]</code>, <code>[3,1,2]</code>, and <code>[3,2,1]</code>.
</p><p></p>
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
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Solution

__This is a very classic question__. 

__One solution__ is to recursively push elements into a list, until all elements are pushed. Make use of a 'visited' array. 

__Another solution__ is using 2 nested for-loops to keep adding next elements. Read [this post](http://www.programcreek.com/2013/02/leetcode-permutations-java/): 

> Loop through the array, in each iteration, a new number is added to different locations of results of previous iteration. Start from an empty List.

Keep in mind: this type of permutation questions always requires insert/delete before/after a recursion.

In case you are interested, there is a __third solution, swap element method__. It is also explained in [the same post](http://www.programcreek.com/2013/02/leetcode-permutations-java/): 

> Swap each element with each element after it.

### My code 

__Adding elements one by one__ (recommended)

    public class Solution {
        public List<List<Integer>> permute(int[] num) {
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

__The double nested for-loop method__

    public class Solution {
        public ArrayList<ArrayList<Integer>> permute(int[] num) {
            ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();

            //start from an empty list
            result.add(new ArrayList<Integer>());

            for (int i = 0; i < num.length; i++) {
                //list of list in current iteration of the array num
                ArrayList<ArrayList<Integer>> current = new ArrayList<ArrayList<Integer>>();

                for (ArrayList<Integer> l : result) {
                    // # of locations to insert is largest index + 1
                    for (int j = 0; j < l.size()+1; j++) {
                        // + add num[i] to different locations
                        l.add(j, num[i]);
                        ArrayList<Integer> temp = new ArrayList<Integer>(l);
                        current.add(temp);
                        l.remove(j);
                    }
                }
                result = new ArrayList<ArrayList<Integer>>(current);
            }
            return result;
        }
    }

__The swap element method__

    public class Solution {
        public ArrayList<ArrayList<Integer>> permute(int[] num) {
            ArrayList<ArrayList<Integer>> result = new ArrayList<ArrayList<Integer>>();
            permute(num, 0, result);
            return result;
        }

        void permute(int[] num, int start, ArrayList<ArrayList<Integer>> result) {

            if (start >= num.length) {
                ArrayList<Integer> item = convertArrayToList(num);
                result.add(item);
            }

            for (int j = start; j <= num.length - 1; j++) {
                swap(num, start, j);
                permute(num, start + 1, result);
                swap(num, start, j);
            }
        }

        private ArrayList<Integer> convertArrayToList(int[] num) {
            ArrayList<Integer> item = new ArrayList<Integer>();
            for (int h = 0; h < num.length; h++) {
                item.add(num[h]);
            }
            return item;
        }

        private void swap(int[] a, int i, int j) {
            int temp = a[i];
            a[i] = a[j];
            a[j] = temp;
        }
    }
