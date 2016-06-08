---
layout: post
title: "[LeetCode 129] Sum Root to Leaf Numbers"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/sum-root-to-leaf-numbers/)

<div class="question-content">
            <p></p><p>Given a binary tree containing digits from <code>0-9</code> only, each root-to-leaf path could represent a number.</p>
<p>An example is the root-to-leaf path <code>1-&gt;2-&gt;3</code> which represents the number <code>123</code>.</p>

<p>Find the total sum of all root-to-leaf numbers.</p>

<p>For example,
</p><pre>    1
   / \
  2   3
</pre>
<p></p>
<p>
The root-to-leaf path <code>1-&gt;2</code> represents the number <code>12</code>.<br>
The root-to-leaf path <code>1-&gt;3</code> represents the number <code>13</code>.
</p>
<p>
Return the sum = 12 + 13 = <code>25</code>.
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
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="white">10 minutes</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is DFS standard question__. 

### Solution

I posted 2 pieces of my code, and 1 best code (from [this blog](http://blog.sina.com.cn/s/blog_b9285de20101iv6l.html)). 

### Code

__First, my solution using List__. 

    int sum = 0;
    
    public int sumNumbers(TreeNode root) {
        dfs(root, new LinkedList<Integer>());
        return sum;
    }
    
    private void dfs(TreeNode node, LinkedList<Integer> list) {
        if (node == null) return;
        if (node.left == null && node.right == null) {
            int num = 0;
            for (int i = 0; i < list.size(); i ++) 
                num = num * 10 + list.get(i);
            sum += num * 10 + node.val;
            return;
        }
        // if node is not null, not a leaf
        list.add(node.val);
        dfs(node.left, list);
        dfs(node.right, list);
        list.remove(list.size() - 1);
    }

__Second, previous code refactored, without using list__, because it's not necessary to know the previous path. 

    int sum = 0;
    public int sumNumbers(TreeNode root) {
        dfs(root, 0);
        return sum;
    }
    
    private void dfs(TreeNode node, int preVal) {
        if (node == null) return;
		int curVal = preVal * 10 + node.val;
        if (node.left == null && node.right == null) {
            int num = 0;
            sum += curVal;
            return;
        }
        // if node is not null, not a leaf
        dfs(node.left, curVal);
        dfs(node.right, curVal);
    }

__Third, best solution__

    public int sumNumbers(TreeNode root) {
        return dfs(root,0);
    }

    int dfs(TreeNode root, int sum){
        if(root==null) return 0;
        sum=sum*10+root.val;
        if(root.left==null && root.right==null) return sum;
        return dfs(root.left,sum) + dfs(root.right,sum);
    }
