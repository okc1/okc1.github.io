---
layout: post
title: "[Fundamental] Suffix Tree "
comments: true
categories:
- Fundamental
- z-string-search

---

[ref](http://www.geeksforgeeks.org/pattern-searching-set-8-suffix-tree-introduction/)

### Suffix tree

Both KMP Algorithm and Rabin Karp Algorithm __pre-process the pattern__ to make the pattern searching faster. The best time complexity that we could get by preprocessing pattern is __O(n), where n is length of the text__. 

Now we will discuss an approach that __pre-processes the text__. A suffix tree is built of the text. After preprocessing text (building suffix tree of text), we can __search any pattern in O(m) time__ where m is length of the pattern.

Though search is very fast - just proportional to length of the pattern, it may become costly if __the text changes frequently__. It is good for fixed text or less frequently changing text though.

#### Suffix Tree VS. Trie

__A Suffix Tree is a compressed trie of all suffixes of the given text__. 

#### Compressed Trie

__A Compressed Trie__ is obtained from standard trie by joining chains of single nodes. 

Example, a standard trie: 

{% img middle /assets/images/standardtrieNew.png %}

A Compressed Trie: 

{% img middle /assets/images/CompressedTrieNew.png %}

#### build a Suffix Tree

1. Generate all suffixes of given text.
1. Consider all suffixes as individual words and build a compressed trie.

Eg.

    banana\0
    anana\0
    nana\0
    ana\0
    na\0
    a\0
    \0

Example question: __[CC150v4] 20.8 Full Text Search (Suffix Tree)__
