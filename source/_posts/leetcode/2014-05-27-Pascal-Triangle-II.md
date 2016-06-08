---
layout: post
title: "[LeetCode 119] Pascal's Triangle II"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/pascals-triangle-ii/)

<div class="question-content">
            <p></p><p>Given an index <i>k</i>, return the <i>k</i><sup>th</sup> row of the Pascal's triangle.</p>

<p>
For example, given <i>k</i> = 3,<br>
Return <code>[1,3,3,1]</code>.
</p>

<p>
<b>Note:</b><br>
Could you optimize your algorithm to use only <i>O</i>(<i>k</i>) extra space?
</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="lime"></td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a math question__. 

First code below is my code. 

Second code is a very concise solution from [this blog](http://xiaotong-blog.herokuapp.com/posts/16). 

### Code

__First, my code__

    public ArrayList<Integer> getRow(int rowIndex) {
		ArrayList<Integer> ans = new ArrayList<Integer>();
		if (rowIndex == 0) {
			ans.add(1);
			return ans;
		}
		int[] nodes = new int[rowIndex + 1];
		nodes[0] = 1;
		for (int k = 1; k <= rowIndex; k++) {
			for (int i = k / 2; i >= 1; i--) {
				if (k % 2 == 0 && i == k / 2)
					nodes[i] = 2 * nodes[i - 1];
				else
					nodes[i] = nodes[i - 1] + nodes[i];
			}
			for (int j = k / 2 + 1; j <= k; j++) {
				nodes[j] = nodes[k - j];
			}
		}
		for (Integer a: nodes) ans.add(a);
		return ans;
	}

__Second, a better version__

    public ArrayList<Integer> getRow(int rowIndex) {
        ArrayList<Integer> ans = new ArrayList<Integer>();
        for (int j = 0; j <= rowIndex; j ++){
            for (int i = 1; i < ans.size(); i ++)
                ans.set(i-1, ans.get(i-1)+ans.get(i));
            ans.add(0,1);
        }
        return ans;
    }
