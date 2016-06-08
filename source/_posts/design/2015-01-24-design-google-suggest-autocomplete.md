---
layout: post
title: "[Design] Design Google Suggest (autocomplete) "
comments: true
category: Design

---

### Overview 

__Google Suggest__ was [launched in 2004](http://googleblog.blogspot.sg/2004/12/ive-got-suggestion.html) as a 20% time project from Google engineer Kevin Gibbs. He developed the idea on a [Google shuttle bus](http://www.theatlantic.com/technology/archive/2013/08/how-googles-autocomplete-was-created-invented-born/278991/).

### Design

1. Use trie. 
1. Use cache (distributed cache)

#### Trie

Just make use of all keywords (including space) and build a trie out of it. Then you are good to go just search in Trie. 

A comparison of speed between DB, Set and Trie can be found [here](http://sujitpal.blogspot.sg/2007/02/three-autocomplete-implementations.html). A lot of implementation code can be found [here](http://stackoverflow.com/questions/7058724/how-to-create-an-efficient-auto-complete). 

#### Memcached

Distributed caching + LRU replacement algorithm. Refer to __[Design] Distributed Caching - memcached__ for more. 
