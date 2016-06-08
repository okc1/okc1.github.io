---
layout: post
title: "[NineChap 9] Big Date, System Design and Resume (`)"
comments: true
category: NineChap
---

## Resume

1. Do not write anything unrelated to CS. 
1. Do not write too long - 1 or 2 pages are fine. Senior engineer 3 pages. 
1. Do not write low GPA
1. Never ever write "proficient in anything"

## Big Data

Most classic question is "Frequent items" (refer to July's blog). 

### Find top k hot queries in a daily access log of Google. 

Variation:

1. k = 1 vs k = 100000 - majority numbers
1. low RAM vs sufficient RAM
1. single machine vs multiple machines
1. accurate vs inaccurate

Sufficient RAM

1. HashTable + Heap (min-heap)
1. Time O(n * logk), Space O(n)

Low RAM

1. Split into 1000 (i.e. LOG/M) files by hash(query) % 1000
1. Using HashTable + Heap to get top k for each files
1. Collect 1000 top k queries and get global top k
1. This method requires a lot of disk access and r/w, still slow. 

Inaccurate (reduce memory from O(n) to O(k))

1. Hash Count (only need to know this one)
    Limit the size of HashMap. The bigger the RAM, the more accurate is the result. 
1. Space Saving
1. Lossy Counting
1. Sticky Sampling
1. Count Sketch

Bloom Filter

1. Regular bloom filter - use 4 线性无关 formula
1. Counting bloom filter - support delete
1. Better DS than HashMap, but can loose some accuracy

Trie

Bitmap

Find all unique queries - use bigmap to store 3 types of states

## System Design

### Design a short url system

1. Cache 

> to store hot urls

1. Load Balance 

> Too many click in short time

1. Storage balance

> Hash value of an url and then store in 
individual machine
>
> Expansibility?

1. Consistent Hash

> Node, can increase # of machines to store information

> Migration process

1. Router

> check which machine response my query
>
> light-weight calculations
>
> what is router is down?

1. Locale

> url frequently access by China, then put the url storage in Beijing

### Need-to-know Design patterns

1. Singleton
1. Factory
1. Master-slave (esp. for relational DB)

[MapReduce: Simplified Data Processing on Large Clusters](http://static.googleusercontent.com/media/research.google.com/en//archive/mapreduce-osdi04.pdf)

[The Google File System](http://static.googleusercontent.com/media/research.google.com/en//archive/gfs-sosp2003.pdf)

[BigTable: A Distributed Storage System for Structured Data](http://static.googleusercontent.com/media/research.google.com/en//archive/bigtable-osdi06.pdf)
