---
layout: post
title: "[Design] Find similar library books "
comments: true
category: Design

---

### Question

[link](http://www.mitbbs.com/article_t/Recommend/31401087.html)

有很大一个电子图书馆，里面每本书的每一页都是OCR转换出来的text，所有每页大
约有5%的error（转换错误，错误分割单词，跳脱。。。）。设计一个方法判定图书馆
里是否有完全一样的书（duplicate），或者将来有书进来时判定同样的书是否已存在。

### Solution

Very large string matching, we mush use __hashing or similar technique__. Since books have error, we need to do __fuzzy search/matching__. Bloom filter is designed to do this! 

Refer to __[Design] Big Data - Fuzzy Search Url (Bloom Filter)__. 
