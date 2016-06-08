---
layout: post
title: "[Fundamental] Implement Trie and Suffix Tree "
comments: true
categories:
- Fundamental
- z-string-search

---

### Trie Node

    public class TrieNode {
        boolean isLeaf;
        TrieNode[] child;

        public TrieNode(boolean isLeaf) {
            this.isLeaf = isLeaf;
            this.child = new TrieNode[26];
        }

        public void insert(String str) {
            if (str == null || str.length() == 0) {
                this.isLeaf = true;
                return;
            }
            char cur = str.charAt(0);
            if (child[cur - 'a'] == null) {
                child[cur - 'a'] = new TrieNode(str.length() == 1);
            }
            child[cur - 'a'].insert(str.substring(1));
        }

        public boolean trieSearch(String str) {
            // have to consider leaf node
            if (str == null || str.length() == 0) {
                return isLeaf;
            }
            char cur = str.charAt(0);
            if (child[cur - 'a'] == null) {
                return false;
            }
            return child[cur - 'a'].trieSearch(str.substring(1));
        }

        public boolean suffixTreeSearch(String str) {
            // suffixTreeSearch don't consider leaf node
            // cuz we search for prefix of suffixes
            if (str == null || str.length() == 0) {
                return true;
            }
            char cur = str.charAt(0);
            if (child[cur - 'a'] == null) {
                return false;
            }
            return child[cur - 'a'].suffixTreeSearch(str.substring(1));
        }
    }

### Trie

    public class Trie {
        TrieNode root;

        public Trie(String[] input) {
            root = new TrieNode(false);

            for (String str : input) {
                root.insert(str);
            }
        }

        public boolean search(String query) {
            return root.trieSearch(query);
        }
    }

#### Suffix Tree

Suffix tree might also consider the __List of indexes__ thing, which I do not take into consideration in my code. 

    public class SuffixTree {
        TrieNode root;

        public SuffixTree(String input) {
            root = new TrieNode(false);

            for (int i = 0; i < input.length(); i++) {
                root.insert(input.substring(i));
            }
        }

        public boolean search(String query) {
            return root.suffixTreeSearch(query);
        }
    }
