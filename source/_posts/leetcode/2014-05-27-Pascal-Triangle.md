---
layout: post
title: "[LeetCode 118] Pascal's Triangle"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/pascals-triangle/)

<div class="question-content">
            <p></p><p>Given <i>numRows</i>, generate the first <i>numRows</i> of Pascal's triangle.</p>

<p>
For example, given <i>numRows</i> = 5,<br>
Return
</p><pre>[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
</pre>
<p></p><p></p>
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

Below is my code. 

### Code

    public ArrayList<ArrayList<Integer>> generate(int numRows) {
        ArrayList<ArrayList<Integer>> ans = new ArrayList<ArrayList<Integer>>();
        if (numRows == 0)
            return ans;
        for (int i = 0; i < numRows; i++){
            ArrayList<Integer> list = new ArrayList<Integer>();
            for (int j = 0; j <= i; j++){
                if (j == 0 || j == i){
                    list.add(1);
                } else {
                    list.add(ans.get(i-1).get(j-1) + ans.get(i-1).get(j));
                }
            }
            ans.add(list);
        }
        return ans;
    }