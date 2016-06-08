---
layout: post
title: "[LeetCode 30] Substring with Concatenation of All Words"
comments: true
category: Leetcode

---

### Question 

[link](http://oj.leetcode.com/problems/substring-with-concatenation-of-all-words/)

<div class="question-content">
            <p></p><p>
You are given a string, <b>S</b>, and a list of words, <b>L</b>, that are all of the same length. Find all starting indices of substring(s) in S that is a concatenation of each word in L exactly once and without any intervening characters.
</p>

<p>
For example, given:<br>
<b>S</b>: <code>"barfoothefoobarman"</code><br>
<b>L</b>: <code>["foo", "bar"]</code>
</p>

<p>
You should return the indices: <code>[0,9]</code>.<br>
(order does not matter).
</p><p></p>
          </div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="white">1</td>
	</tr>
	<tr>
		<td>Diffficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

There are 2 ways to solve this question. 

__The naive approach takes around 1200ms to pass__, and __the KPM-like approach takes around half of that time__. Both methods are explained well in [this blog](http://n00tc0d3r.blogspot.sg/2013/06/substring-with-concatenation-of-all.html).

I will cover only the naive approach. 

### Naive approach

__The naive approach uses a HashMap__ for 2 reasons. Reason 1 is because there can be duplications in L, and reason 2 is the searching is faster. For information on HashMap, refer to __[Fundamental] Recap on Java HashMap__. 

__Time complexity of this solution is O((n - k * m) x m)__, and space is the size of list L, O(m). If m is not very big, the time can be regarded as O(n). 

### My code 

    public class Solution {
        public List<Integer> findSubstring(String S, String[] L) {
            List<Integer> ans = new ArrayList<Integer>();
            if (L == null || L.length == 0 || S == null || S.length() == 0) {
                return ans;
            }
            int num = L.length;
            int len = L[0].length();
            if (num * len > S.length()) {
                return ans;
            }
            // build a hashset, for simplifying the hashmap generation later on
            HashMap<String, Integer> set = new HashMap<String, Integer>();
            for (String str: L) {
                if (set.containsKey(str)) {
                    set.put(str, set.get(str) + 1);
                } else {
                    set.put(str, 1);
                }
            }
            // starting from i, check Concatenation of All Words
            for (int i = 0; i <= S.length() - (num * len); i++) {
                // first build a HashMap from the set that we acquired before
                HashMap<String, Integer> map = new HashMap<String, Integer>(set);
                for (int j = 0; j < num; j++) {
                    String str = S.substring(i + j * len, i + (j + 1) * len);
                    if (!map.containsKey(str)) {
                        break;
                    } else if (map.get(str) > 1) {
                        map.put(str, map.get(str) - 1);
                    } else if (map.get(str) == 1) {
                        map.remove(str);
                    }
                }
                if (map.isEmpty()) {
                    ans.add(i);
                }
            }
            return ans;
        }
    }
