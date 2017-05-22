---
layout: post
title: "[Question] Trie Wildcard String Matching"
comments: true
categories:
- Question
- z-string-search
tags: [  ]
---

# Question

[link](https://discuss.leetcode.com/topic/54332/wildcard-on-trie/2)

> Given a trie data struture, implement add() and search() method, which support wildcard matching.

eg. If trie contains ["cool", "kid", "kindle", "kind"]

These would match: "co*l", "kind", "***"

These won't: "**", "kid*", "coo"

# Solution

First, know how to build a trie, then know how to search in Trie. This could be tricky. Do Read On!

1. Trie (root) start with an empty node. 
2. When do searching, __ALWAYS assumes that current TrieNode is matched__. I.e. do not check value of current TrieNode. Instead, check current TrieNode's children, and find a match.
3. The only case __you return true__, is when matching reaches current TrieNode, and __current TrieNode is an terminating node for a word__. 
4. Be careful and __do not confuse yourself__ for which node you gonna match, and when you return true. 

Read the code below. If you still have a hard time, read #2 and #3 above, again. 


# Code

	public boolean solve(TrieRoot trie, String word) {
		if (word == null || word.length() == 0) {
			return false;
		}
		return matchFromChildren(trie.getRoot(), word, 0);
	}
	
	private boolean matchFromChildren(TrieNode node, String word, int index) {
		// [important note] 
		// regardless of the value of node.letter, match word[index...] from node.children
		
		if (index > word.length()) {
			// impossible to reach here
			return false;
		} else if (index == word.length()) {
			// word is now fully matched, check if isTerminalNode(node)
			return node.isEndOfWord();
		}
		
		char curLetter = word.charAt(index);
		if (curLetter == '*') {
			for (TrieNode child: node.getAllChildren()) {
				if (matchFromChildren(child, word, index + 1)) {
					return true;
				}
			}
			return false;
		} else {
			TrieNode nextNode = node.getChild(curLetter);
			if (nextNode == null) {
				return false;
			} else {
				return matchFromChildren(nextNode, word, index + 1);
			}
		}
	}
