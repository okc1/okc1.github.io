---
layout: post
title: "[LeetCode 126] Word Ladder II (unsolvable)"
comments: true
category: Leetcode
tags: [ unsolvable ]
---

### Question 
[link](https://oj.leetcode.com/problems/word-ladder-ii/)

<div class="question-content">
            <p></p><p>
Given two words (<i>start</i> and <i>end</i>), and a dictionary, find all shortest transformation sequence(s) from <i>start</i> to <i>end</i>, such that:
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
Return<br>
</p><pre>  [
    ["hit","hot","dot","dog","cog"],
    ["hit","hot","lot","log","cog"]
  ]
</pre>
<p></p>

<p>
<b>Note:</b><br>
</p><ul>
<li>All words have the same length.</li>
<li>All words contain only lowercase alphabetic characters.</li>
</ul>
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
		<td bgcolor="white">1</td>
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

__This is an unsolvable question__. 

### Solution

A solution is available [here](http://blog.csdn.net/whuwangyi/article/details/21611433), but I did not solved it and I gave up.

### Code

    public class Node {  
        public int dist;  
        public String str;  
        public LinkedList<Node> prev;  
      
        public Node(int dist, String str) {  
            this.dist = dist;  
            this.str = str;  
            this.prev = new LinkedList<Node>();
        }
      
        public void addPrev(Node pNode) {  
            prev.add(pNode);  
        }  
    }  
      
    public ArrayList<ArrayList<String>> findLadders(String start,  
            String end, HashSet<String> dict) {  
        dict.add(end);  
      
        // Key: the dictionary string; Value: Node  
        Map<String, Node> map = new HashMap<String, Node>();  
        Queue<String> queue = new LinkedList<String>();  
      
        Node startNode = new Node(1, start);  
        queue.offer(start);  
        map.put(start, startNode);  
      
        ArrayList<ArrayList<String>> ret = new ArrayList<ArrayList<String>>();  
      
        while (!queue.isEmpty()) {  
            String str = queue.poll();  
      
            if (str.equals(end)) {  
                getPaths(map.get(end), map, new ArrayList<String>(), ret);  
                return ret;  
            }  
      
            for (int i = 0; i < str.length(); i++) {  
                for (int j = 0; j <= 25; j++) {  
                    // transform it into another word  
                    String newStr = replace(str, i, (char) ('a' + j));  
      
                    // if a new word is explored  
                    if (dict.contains(newStr)) {  
                        if (!map.containsKey(newStr)) {  
                            // construct a new node  
                            Node node = map.get(str);  
                            Node newNode = new Node(node.dist + 1, newStr);  
                            newNode.prev = new LinkedList<Node>();  
                            newNode.prev.add(node);  
      
                            map.put(newStr, newNode);  
                            queue.offer(newStr);  
                        } else {  
                            Node node = map.get(newStr);  
                            Node prevNode = map.get(str);  
      
                            // increase the path set  
                            if (node.dist == prevNode.dist + 1) {  
                                node.addPrev(prevNode);  
                                // queue.offer(newStr); // will cause TLE!!!  
                            }  
                        }  
                    }  
                }  
            }  
        }  
      
        return ret; // return an empty set  
    }  
      
    // replace the index of the given string with the given char  
    private String replace(String str, int index, char c) {  
        StringBuilder sb = new StringBuilder(str);  
        sb.setCharAt(index, c);  
        return sb.toString();  
    }  
      
    // get all the paths by using DFS  
    private void getPaths(Node end, Map<String, Node> map,  
            ArrayList<String> curPath, ArrayList<ArrayList<String>> paths) {  
        if (end == null) {  
            paths.add(curPath);  
            return;  
        }  
      
        curPath.add(0, end.str);  
        if (!end.prev.isEmpty()) {  
            for (Node prevNode : end.prev) {  
                getPaths(prevNode, map, new ArrayList<String>(curPath), paths);  
            }  
        } else {  
            getPaths(null, map, curPath, paths);  
        }  
    }
