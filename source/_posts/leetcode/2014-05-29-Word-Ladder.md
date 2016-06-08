---
layout: post
title: "[LeetCode 127] Word Ladder"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/word-ladder/)

<div class="question-content">
            <p></p><p>
Given two words (<i>start</i> and <i>end</i>), and a dictionary, find the length of shortest transformation sequence from <i>start</i> to <i>end</i>, such that:
</p>
<ol>
<li>Only one letter can be changed at a time</li>
<li>Each intermediate word must exist in the dictionary</li>
</ol>

<p>
For example,
</p>
<p>
Given:<br>
<i>start</i> = <code>"hit"</code><br>
<i>end</i> = <code>"cog"</code><br>
<i>dict</i> = <code>["hot","dot","dog","lot","log"]</code><br>
</p>
<p>
As one shortest transformation is <code>"hit" -&gt; "hot" -&gt; "dot" -&gt; "dog" -&gt; "cog"</code>,<br>
return its length <code>5</code>.
</p>

<p>
<b>Note:</b><br>
</p><ul>
<li>Return 0 if there is no such transformation sequence.</li>
<li>All words have the same length.</li>
<li>All words contain only lowercase alphabetic characters.</li>
</ul>
<p></p><p></p>
</div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is an extremely difficult question__.

### Solution

1. This question is __find shortest path__, so we shall choose __BFS__ over DFS. 

2. Since finding an element in HashSet is O(1) time, __we can generate all the possible strings of distance = 1__ and check if they are in the dictionary. In this way, we reduce time complexity from O(m x n) to O(m x 26). 

3. If a word is found from the dictionary, remove it. 

__For the 3rd point, we remove the word from dict__. It might be hard to understand. [This blog](http://blog.csdn.net/zxzxy1988/article/details/8591890) explains it clear enough. 

<blockquote cite="http://blog.csdn.net/zxzxy1988/article/details/8591890">
另外一个需要注意的地方就是，如果我们曾经遍历过某个元素，我会将其从字典中删除，以防以后再次遍历到这个元素。这里有几种情况：<br><br>
1.以后再也遍历不到这个元素，那么我们删除它当然没有任何问题。<br><br>
2.我们以后会遍历到该元素，又分为两种情况：<br><br>
(1)在本层我们就能遍历到该元素。也就是说，我们到达这个元素有两条路径，而且它们都是最短路径。<br><br>
对于本题来说，是没有什么影响的，因为到dog距离都是3，到dig距离都是4。但是后面我们做word ladder 2的时候，如果没有考虑这个情况，将是非常致命的，因为题目要求输出最短路径的所有情况<br><br>
(2)在更下层我们才能够遍历到该元素。比如hot-&gt;dot-&gt;dog-&gt;dig和hot-&gt;hat-&gt;dat-&gt;dag-&gt;dog-&gt;dig，如果第一次我们找到了dog并且将其删除，那么第二次我们实际上是找不到这个元素的。这样对于本题来说，没有任何影响。对于word ladder 2来说，因为也是要输出最短路径，所以也不会有任何影响。<br><br>
</blockquote>

### Code

__BFS solution__

This is similar to the code posted in [this article](http://www.programcreek.com/2012/12/leetcode-word-ladder/). 

	public int ladderLength(String start, String end, HashSet<String> dict) {
		if (start.equals(end)) return 1;
		LinkedList<String> words = new LinkedList<String>();
		LinkedList<Integer> nums = new LinkedList<Integer>();
		words.add(start);
		nums.add(1);
		while (!words.isEmpty()) {
			String word = words.remove();
			int num = nums.remove();
			// otherwise, change each char in word, and find it from dict
			char[] charArr = word.toCharArray();
			for (int i = 0; i < charArr.length; i++) {
				char originChar = charArr[i];
				for (char j = 'a'; j <= 'z'; j++) {
					charArr[i] = j;
					String newWord = new String(charArr);
					if (newWord.equals(end))
						return num + 1;
					if (dict.contains(newWord)) {
						dict.remove(newWord);
						words.add(newWord);
						nums.add(num + 1);
					}
				}
				charArr[i] = originChar;
			}
		}
		return 0;
	}
