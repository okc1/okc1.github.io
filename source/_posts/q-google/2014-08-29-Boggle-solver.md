---
layout: post
title: "[Google] Boggle Solver (search words from matrix)"
comments: true
categories:
- q-google
- z-string-search

---

### Question 

[link](http://stackoverflow.com/questions/746082/how-to-find-list-of-possible-words-from-a-letter-matrix-boggle-solver)

> Boggle Game: 

    F X I E
    A M L O
    E W B X
    A S T U

> The goal of the game is to find as many words as you can that can be formed by chaining letters together. You are given a dictionary of words are reference. 

### Solution

__[The best solution](http://stackoverflow.com/a/4314056) is to use Trie__, then do DFS search. 

The idea is from [this answer](http://stackoverflow.com/a/746102) (however, this guy said his solution does not handle 'visited' nodes properly, meaning that same char might be visited again to produce a word). 

We need to first define a class called Item: 

    class Item {
        public final int x, y;
        public final String prefix;

        public Item(int row, int column, String prefix) {
            this.x = row;
            this.y = column;
            this.prefix = prefix;
        }
    }

So when we start doing DFS, we pass in an Item object which stores 2 information: 

1. The next position that we're going to visit.
1. The prefix string that we have validated so far (before visiting this position).

For example: 

    F X I E
    A M L O
    E W B X
    A S T U

We'll have Items objects like (0, 0, ""), (0, 1, "F"), (0, 2, "FA") ... We guarantee that the prefix must be a valid prefix by searching them in the Trie. 

How to tell whether a string is a prefix of word, or it's an actual word? We have a property in TrieNode called TrieNode.isWord() to help us. 

The code I wrote below is based on [this Java solution by zouzhile](http://stackoverflow.com/a/11698898). 

### Code

BoggleSolver.java

    public class BoggleSolver {

        private static BufferedReader in = null;
        private static final String INPUT_FILE = "dictionary.txt";

        public static void beginFileReader() {
            try {
                in = new BufferedReader(new FileReader(new File(BoggleSolver.class
                        .getResource(INPUT_FILE).toURI())));
            } catch (FileNotFoundException e) {
                e.printStackTrace();
            } catch (URISyntaxException e) {
                e.printStackTrace();
            }
        }

        private Trie buildTrie() {
            Trie trie = new Trie();
            beginFileReader();
            String line = null;
            try {
                while ((line = in.readLine()) != null) {
                    String[] words = line.split(" ");
                    for (String word : words) {
                        word = word.trim().toLowerCase();
                        trie.addWord(word);
                    }
                }
                if (in != null) {
                    in.close();
                }
            } catch (IOException e1) {
                e1.printStackTrace();
            }
            return trie;
        }

        public Set<String> findWords(char[][] map, Trie dict) {
            Set<String> ans = new TreeSet<String>();
            int m = map.length;
            int n = map[0].length;
            for (int i = 0; i < m; i++) {
                for (int j = 0; j < n; j++) {
                    boolean[][] visited = new boolean[m][n];
                    findWordsDfs(ans, dict, map, visited, new Item(i, j, ""));
                    // item have 3 parameters:
                    // location x,y and the prefix string before reaching (i.j)
                }
            }
            return ans;
        }

        public void findWordsDfs(Set<String> ans, Trie dict, char[][] map,
                boolean[][] visited, Item item) {
            // item: the location that we're going to test
            // item.prefix is the word prefix before reaching (x, y)

            int m = map.length;
            int n = map[0].length;
            int x = item.x;
            int y = item.y;

            // check whether cur.(x,y) is a valid position
            if (x < 0 || x >= m || y < 0 || y >= n) {
                return;
            } else if (visited[x][y]) {
                return;
            }
            String newWord = item.prefix + map[x][y];
            // check whether cur.prefix is a valid prefix
            TrieNode findWord = dict.match(newWord);
            if (findWord == null) {
                // up to this position (x, y), the word dont' exists
                return;
            }
            // now cur is in a valid position, with a valid prefix
            if (findWord.isWord()) {
                ans.add(newWord);
            }
            // visit this position, and continue in 4 different directions
            visited[x][y] = true;
            findWordsDfs(ans, dict, map, visited, new Item(x, y - 1, newWord));
            findWordsDfs(ans, dict, map, visited, new Item(x, y + 1, newWord));
            findWordsDfs(ans, dict, map, visited, new Item(x - 1, y, newWord));
            findWordsDfs(ans, dict, map, visited, new Item(x + 1, y, newWord));
            visited[x][y] = false;
        }

        public static void main(String[] args) {
            String[] rows = "eela,elps,weut,korn".split(",");
            char[][] input = new char[4][4];
            for (int i = 0; i < 4; i++) {
                input[i] = rows[i].toCharArray();
            }

            // prepare test data
            BoggleSolver solver = new BoggleSolver();
            Trie dictionary = solver.buildTrie();
            // start finding words
            Set<String> set = solver.findWords(input, dictionary);
            // present the result
            System.out.println(set.size() + " words are found, they are: ");
            for (String str : set) {
                System.out.println(str);
            }
        }

        class Item {
            public final int x, y;
            public final String prefix;

            public Item(int row, int column, String prefix) {
                this.x = row;
                this.y = column;
                this.prefix = prefix;
            }
        }
    }

Trie.java

    public class Trie {
        private TrieNode root;

        public Trie() {
            this.root = new TrieNode();
        }

        public void addWord(String word) {
            TrieNode node = this.root;
            for (char c : word.toCharArray()) {
                node = node.addChild(c);
                if (node == null)
                    return;
            }
            node.setWord(true);
        }

        public TrieNode match(String s) {
            TrieNode node = this.root;
            for (char c : s.toCharArray()) {
                node = node.get(c);
                if (node == null)
                    return null;
            }
            return node;
        }
    }

TrieNode.java

    public class TrieNode {
        private TrieNode[] children;
        private boolean isWord = false;

        public TrieNode() {
            this.children = new TrieNode[26];
        }

        public TrieNode addChild(char child) {
            if (child < 'a' || child > 'z')
                return null;

            int offset = child - 'a';
            if (this.children[offset] == null) {
                this.children[offset] = new TrieNode();
            }
            return this.children[offset];
        }

        public boolean isWord() {
            return isWord;
        }

        public void setWord(boolean isWord) {
            this.isWord = isWord;
        }

        public TrieNode get(char c) {
            int offset = c - 'a';
            return this.children[offset];
        }
    }
