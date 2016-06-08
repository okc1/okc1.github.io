---
layout: post
title: "[Google] Lexicographic order (letter replacement) of dictionary "
comments: true
category: q-google
tags: [ src ]
---

### Question 

[link](http://www.careercup.com/question?id=13394663)

> Given set of words that are lexicographically sorted, return lexicographic order. E.g:

    abc
    acd
    bcc
    bed
    bdc
    dab

> The order of letters for the given example would be

    a->b->c->e->d

### Solution

> Just form a graph(DAG) and do a topological sort. 

Start from the first pair in the dictionary. Compare two strings in this pair __till first mismatch__. 

Eg: __aad & aab__, in this case create an edge __d -> b__. 

More details is available [here](http://codereview.stackexchange.com/questions/48292/return-the-lexicographic-order). 

#### Variant, and a different solution

Another way of asking this question, is:

> 有一个字典因为某种原因每个字符都被替换成一个别的字符了（但还是一一对应)，
但是单词的顺序没有改变，比如

    cat
    coffee
    common

    --> 

    dkc
    dbhhzz
    dbllbq

> 让找出的这个替换的规则（guaranteed to have a unique one)

__Alternative solution__ is to check according to frequencies.

### Code

	public String lexicoOrder(String[] dict) {
		String ans = "";

		// for each pair, maintain 2 HashMap
		HashMap<Character, Integer> incount = new HashMap<Character, Integer>();
		HashMap<Character, List<Character>> connection = new HashMap<Character, List<Character>>();
		for (String str : dict) {
			for (char c : str.toCharArray()) {
				incount.put(c, 0);
				connection.put(c, new ArrayList<Character>());
			}
		}
		buildGraph(dict, incount, connection);

		// start topology sorting
		Queue<Character> temp = new LinkedList<Character>();
		for (char c : incount.keySet()) {
			if (incount.get(c) == 0) {
				temp.offer(c);
				incount.remove(c);
				// remove any node whose incount is 0
			}
		}
		while (!temp.isEmpty()) {
			char top = temp.poll();
			ans += top;
			// 'top' is next char in line. remove it and delete connections
			List<Character> inNodes = connection.get(top);
			for (char c : inNodes) {
				// remove incount for all nodes from inNodes
				incount.put(c, incount.get(c) - 1);
				if (incount.get(c) == 0) {
					incount.remove(c);
					temp.offer(c);
				}
			}
		}
		if (incount.size() == 0)
			return ans;
		else
			return "unable to find a valid char sequence.";
	}

	public void buildGraph(String[] dict, HashMap<Character, Integer> incount,
			HashMap<Character, List<Character>> connection) {
		// build the graph map
		// abc
		// acd
		// bcc
		// bed
		// bdc
		// dab
		for (int i = 0; i < dict.length - 1; i++) {
			// compare dict[i] and dict[i+1]
			String str1 = dict[i];
			String str2 = dict[i + 1];
			int p = 0;
			while (p < str1.length() && p < str2.length()) {
				if (str1.charAt(p) == str2.charAt(p)) {
					p++;
				} else {
					break;
				}
			}
			if (p == str1.length()) {
				// this is special case eg. "ab" & "abc"
				// this will not give up any information about lexico order
				continue;
			}
			char from = str1.charAt(p);
			char to = str2.charAt(p);
			// update incount
			incount.put(to, incount.get(to) + 1);
			// update connection
			connection.get(from).add(to);
		}
	}
