---
layout: post
title: "[CC150v4] 20.8 Full Text Search (suffix tree) "
comments: true
categories:
- CC150v4
- z-string-search

---

### Question

> Given a string s and an array of smaller strings T, design a method to search s for each small string in T. 

### Solution

__This is a very classic question of string search__, favored by Google and Facebook. 

The solution is __suffix tree__ (to be distinguished from __trie__, or prefix tree, which searched word by its prefix). Suffix tree is good for search a proportion of a long string. For example, using "bibs" to build a suffix tree like this: 

{% img middle /assets/images/suffix-tree-example-bibs.png %}

The building of suffix tree and searching is not a very lengthy code. It's posted below and it's not written by me. 

### Code

Main method:

	public static void main(String[] args) {
		String testString = "mississippi";
		String[] stringList = { "is", "sip", "hi", "sis" };
		SuffixTree tree = new SuffixTree(testString);
		for (String s : stringList) {
			ArrayList<Integer> list = tree.getIndexes(s);
			if (list != null) {
				System.out.println(s + ": " + list.toString());
			} else {
				System.out.println(s + ": does not exist.");
			}
		}
	}

SuffixTree.java

	public class SuffixTree {
		SuffixTreeNode root = new SuffixTreeNode();
		
		public SuffixTree(String s) {
			// create a suffix tree with input string s
			for (int i = 0; i < s.length(); i++) {
				String suffix = s.substring(i);
				root.insertString(suffix, i);
			}
		}
		
		public ArrayList<Integer> getIndexes(String s) {
			return root.getIndexes(s);
		}
	}

SuffixTreeNode.java

	public class SuffixTreeNode {

		char value;
		HashMap<Character, SuffixTreeNode> children;
		ArrayList<Integer> indexes = new ArrayList<Integer>();

		public SuffixTreeNode() {
			children = new HashMap<Character, SuffixTreeNode>();
		}

		public void insertString(String s, int index) {
			indexes.add(index);
			if (s != null && s.length() > 0) {
				value = s.charAt(0);
				SuffixTreeNode child = null;
				if (children.containsKey(value)) {
					child = children.get(value);
				} else {
					child = new SuffixTreeNode();
					children.put(value, child);
				}
				String remainder = s.substring(1);
				child.insertString(remainder, index);
			}
		}

		public ArrayList<Integer> getIndexes(String s) {
			if (s == null || s.length() == 0) {
				return indexes;
			} else {
				char first = s.charAt(0);
				if (children.containsKey(first)) {
					String remainder = s.substring(1);
					return children.get(first).getIndexes(remainder);
				}
			}
			return null;
		}
	}
