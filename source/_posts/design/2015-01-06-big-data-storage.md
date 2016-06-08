---
layout: post
title: "[Design] Big Data Storage "
comments: true
category: Design

---

[ref](http://www.mitbbs.com/article/JobHunting/32580869_0.html)

### Question

__Given 1 trillion messages__ on fb and each message has at max 10 words. 

How do you build the __index table__ and how many machines do you need on the __cluster__ to store the index table?

### One possible answer

Total data = 1 trillion * 10 words * 6 bytes / word = 60TB = one small NetApp box

__Index by hashed userid__; will distribute traffic effectively across servers; cache active users recent messages in memory. 

[Cannot use Netapp box](http://www.glassdoor.com/Interview/Given-a-set-of-n-jobs-with-start-time-end-time-cost-find-a-subset-so-that-no-2-jobs-overlap-and-the-cost-is-maximum-QTN_440168.htm). From what I read in FB engg blog, they have all the info in main memory of server.

Total data = 1 trillion * 10 words * 6 bytes / word = 60TB + 1TB for Indexes.

Considering servers have 64 GB ram. 61 GB usable to store index, 1000 servers. 

#### For more information

Read 2 other posts: __[Design] Distributed hash table__ and __[Design] Cloud, Grid and Cluster__. 
