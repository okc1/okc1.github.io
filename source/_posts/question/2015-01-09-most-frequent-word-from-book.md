---
layout: post
title: "[Question] Most Frequent Word from a book "
comments: true
categories:
- Question
- z-string-search

---

### Question

[link](http://www.careercup.com/question?id=5715664853532672)

> Let's say I gave you a long String and I wanted you to tell me the most common word in that String. How would you do that? 

> Follow-up: how about if I gave you the entire works of Alexandre Dumas, one of the most prolific authors in history. How would your solution work? How could you change it to solve this more specific problem? 

### Solution

There are 2 solutions. Either __HashMap__ or __Trie__. It's easy to think of first, but remember that Trie is designed to do this kind of job. 

> A trie will be more useful in the second situation where you will have millions of words. You can have a counter at every node to see its frequency

__Now the follow up__. For big data problems, we can always do __divide and conquer__ by hash value. 

Alternatively, the comment by [Prince](http://www.careercup.com/question?id=5715664853532672) mentioned how to solve with __Map Reduce__: 

> Instead of loading it as a string first I would stream data so that I avoid memory spike. Further our map size might increases as new words are added to it. Also, we can use map reduce type job were we create map<word, frequency> of each play in parallel and later join/collapse them this will reduce the time it will take to get result. 

> Common phrase should be no different then above algorithm. However we need to rebuild our index with <phase, frequency>
