---
layout: post
title: "[Fundamental] Prefix Tree "
comments: true
categories:
- Fundamental
- z-string-search

---

[ref](http://www.geeksforgeeks.org/trie-insert-and-search/)

### Prefix tree

1. Building a well balanced BST needs time proportional to M * log N, where M is maximum string length and N is number of keys in tree. 
1. Using trie, search in O(M) time. 
1. The penalty is on trie storage requirements.

### Implementation

1. Every node of trie consists of multiple branches. 
1. Each branch represents a possible character of keys. 
1. Mark the last node of every key as leaf node. 

	struct trie_node
	{
		int value; /* Used to mark leaf nodes */
		trie_node_t *children[ALPHABET_SIZE];
	};

Note that a __non-terminating node can also be marked as leaf__. Eg. 

                       root
                    /   \    \
                    t  'a'    b
                    |   |     |
                    h   n    'y'
                    |   |  \    \
                   'e'  s  'y'  'e'
                 /  |   |
                i   r   w
               /    |   |
             'r'   'e'  e
                        |
                       'r'

The leaf nodes are quoted in ''.

Insert and search costs __O(key_length)__, however the memory requirements of trie is __O(ALPHABET_SIZE * key_length * N)__ where N is number of keys in trie. 

__Compressed trie__, ternary search tree, etc. can be used to minimize memory requirements of trie. 
