---
layout: post
title: "[LeetCode 138] Copy List with Random Pointer"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/copy-list-with-random-pointer/)

<div class="question-content bg-color bg-img font-color">
            <p class="font-color"></p><p class="font-color">
A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.
</p>

<p class="font-color">
Return a deep copy of the list.
</p><p class="font-color"></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">20 minutes</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is not a difficult question__, however I mark it as difficulty level "4" because there are 2 solution, the second of which is hard to think of. 

### Solution

__Solution 1 which is my initial idea is using HashMap__ to store mappings from original nodes to copied nodes. This solution become exactly same as another question "Clone Graph", only easier. It works fine.

However such solution uses O(n) extra space. Can we do it with less space? 

__Solution 2 is a in-place method__ which directly creates the copied list. It is well explained in [here](http://www.geeksforgeeks.org/a-linked-list-with-next-and-arbit-pointer/): 

> 1. Create a copy of first node and insert it between Node 1 & Node 2 in original list. Then create a copy of second node and insert it between Node 2 & Node 3... Continue in this fashion
> 2. Set random link of the copied nodes (by referring to __original.random.next__)
> 3. Restore the original and copied lists (and return answer)

This solution (although uses 3 while-loops) is O(n) and O(1) extra space. 

### Code

__First, my solution using HashMap__

    public RandomListNode copyRandomList(RandomListNode head) {
        if (head == null) return null;
        RandomListNode newHead = new RandomListNode(head.label);
        HashMap<RandomListNode, RandomListNode> map = 
                new HashMap<RandomListNode, RandomListNode>();
        map.put(head, newHead);
        RandomListNode orin = head, cp = newHead;
        while (orin != null) {
            if (orin.next != null) {
                if (!map.containsKey(orin.next))
                    map.put(orin.next, new RandomListNode(orin.next.label));
                cp.next = map.get(orin.next);
            }
            if (orin.random != null) {
                if (!map.containsKey(orin.random))
                    map.put(orin.random, new RandomListNode(orin.random.label));
                cp.random = map.get(orin.random);
            }
            orin = orin.next;
            cp = cp.next;
        }
        return newHead;
    }

__Second, constent space solution__

    public RandomListNode copyRandomList(RandomListNode head)  {
        if (head == null)  {
			return null;
		}
		// copy each node and append right after original node
		RandomListNode p = head;
		while (p != null)  {
			RandomListNode cp = new RandomListNode(p.label);
			cp.next = p.next;
			p.next = cp;
			p = p.next.next;
		}
		// now set random pointer of all copied nodes
		p = head;
		while (p != null)  {
			if (p.random != null)  {
				p.next.random = p.random.next;
			}
			p = p.next.next;
		}
		// now restore original list, and connected all copied nodes
		RandomListNode ans = head.next;
		RandomListNode m = head, n = head.next;
		while (m != null)  {
			if (n.next == null)  {
				m.next = null;
				m = null;
			}
			else  {
				m.next = n.next;
				n.next = n.next.next;
				m = m.next;
				n = n.next;
			}
		}
		return ans;
    }
