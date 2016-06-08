---
layout: post
title: "[LeetCode 133] Clone Graph"
comments: true
category: Leetcode

---

### Question 

[link](https://oj.leetcode.com/problems/clone-graph/)

<div class="question-content bg-color bg-img font-color">

<p class="font-color"></p><p class="font-color">
Clone an undirected graph. Each node in the graph contains a <code>label</code> and a list of its <code>neighbors</code>.
</p>

<div class="bg-color bg-img font-color">
<br>
<b>OJ's undirected graph serialization:</b>

<p class="font-color">
Nodes are labeled uniquely.
</p>

We use <code>#</code> as a separator for each node, and <code>,</code> as a separator for node label and each neighbor of the node.
<p class="font-color"></p>

<p class="font-color">
As an example, consider the serialized graph <code><font color="red">{<font color="black">0</font>,1,2#</font><font color="blue"><font color="black">1</font>,2#</font><font color="green"><font color="black">2</font>,2}</font></code>.
</p>

<p class="font-color">
The graph has a total of three nodes, and therefore contains three parts as separated by <code>#</code>.
</p><ol>
<li>First node is labeled as <code><font color="black">0</font></code>. Connect node <code><font color="black">0</font></code> to both nodes <code><font color="red">1</font></code> and <code><font color="red">2</font></code>.</li>
<li>Second node is labeled as <code><font color="black">1</font></code>. Connect node <code><font color="black">1</font></code> to node <code><font color="blue">2</font></code>.</li>
<li>Third node is labeled as <code><font color="black">2</font></code>. Connect node <code><font color="black">2</font></code> to node <code><font color="green">2</font></code> (itself), thus forming a self-cycle.</li>
</ol>
<p class="font-color"></p>

<p class="font-color">
Visually, the graph looks like the following:
</p><pre class="bg-color bg-img font-color">       1
      / \
     /   \
    0 --- 2
         / \
         \_/
</pre>
<p class="font-color"></p>

</div><p class="font-color"></p>
</div>

### Stats

<table border="2">
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">thought for a while</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a difficult coding question, although the idea is simple__. 

### Solution

Two solution: __BFS (recommended) and DFS__. [This](http://leetcode.com/2012/05/clone-graph-part-i.html) is a good analysis article. 

<blockquote cite="http://leetcode.com/2012/05/clone-graph-part-i.html">
<p>Let’s analyze this further by using the below example:</p>
<div style="text-align: center; margin-bottom: 30px;"> <a href="http://www.leetcode.com/wp-content/uploads/2012/05/graph.png"><img src="http://www.leetcode.com/wp-content/uploads/2012/05/graph.png" alt="" title="graph" width="211" height="84" class="aligncenter size-full wp-image-1365"></a><span style="font-size: x-small;">A simple graph</span></div>
<p>Assume that the starting point of the graph is A. First, you make a copy of node A (A2), and found that A has only one neighbor B. You make a copy of B (B2) and connects A2-&gt;B2 by pushing B2 as A2′s neighbor. Next, you find that B has A as neighbor, which you have already made a copy of. Here, we have to be careful not to make a copy of A again, but to connect B2-&gt;A2 by pushing A2 as B2′s neighbor. But, how do we know if a node has already been copied?</p>
</blockquote>

__Basic idea is to use HashMap to store the already-copied nodes__. 

My first attempt is DFS by making use of a 'visited' Set to mark which node I have copied and which is not. This is a nice idea and it solved the problem neatly. 

But after reading [this article](http://www.programcreek.com/2012/12/leetcode-clone-graph-java/), I realize that __'visited' is not needed for BFS solution__! 

__The trick is, whenever I do a 'HashMap.put(curNode, newNode)', I push 'curNode' to queue__. This very well replaces the functionality of the 'visited' set. It also guarantees that when I pop a new element from the queue, __I CAN ALWAYS FIND ITS CORRESPONDING COPY__ from the HashMap - always there. 

### Code

__First, my DFS code__

	public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
	    if (node == null) return null;
		UndirectedGraphNode newNode = new UndirectedGraphNode(node.label);
		HashMap<Integer, UndirectedGraphNode> map = 
		    new HashMap<Integer, UndirectedGraphNode>();
		map.put(node.label, newNode);
		copy(node, newNode, map, new HashSet<Integer>());
		return newNode;
	}

	private void copy(UndirectedGraphNode orin, UndirectedGraphNode cp,
			HashMap<Integer, UndirectedGraphNode> map,
			HashSet<Integer> visited) {
		if (visited.contains(orin.label))
			return;
		else
			visited.add(orin.label);
		for (UndirectedGraphNode n : orin.neighbors) {
			if (map.containsKey(n.label)) {
				cp.neighbors.add(map.get(n.label));
			} else {
				UndirectedGraphNode newNode = new UndirectedGraphNode(n.label);
				map.put(n.label, newNode);
				cp.neighbors.add(map.get(n.label));
			}
		}
		// do DFS recursively
		for (int i = 0; i < orin.neighbors.size(); i++) {
			copy(orin.neighbors.get(i), cp.neighbors.get(i), map, visited);
		}
	}

__Second, my BFS code without using 'visited' HashSet__

	public UndirectedGraphNode cloneGraph(UndirectedGraphNode node) {
		if (node == null) return null;
		HashMap<UndirectedGraphNode, UndirectedGraphNode> map 
		        = new HashMap<UndirectedGraphNode, UndirectedGraphNode>();
		map.put(node, new UndirectedGraphNode(node.label));
		LinkedList<UndirectedGraphNode> queue = new LinkedList<UndirectedGraphNode>();
		queue.add(node);
		// queue is guaranteed to always have non-traversed nodes
		while ( !queue.isEmpty() ) {
		    UndirectedGraphNode orin = queue.remove();
		    UndirectedGraphNode cp = map.get(orin);
		    for (UndirectedGraphNode n : orin.neighbors) {
    			if ( !map.containsKey(n) ) {
    				map.put(n, new UndirectedGraphNode(n.label));
					queue.add(n);
    			}
				UndirectedGraphNode newNode = map.get(n);
				cp.neighbors.add(newNode);
    		}
		}
		return map.get(node);
	}
