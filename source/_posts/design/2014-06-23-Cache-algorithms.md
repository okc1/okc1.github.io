---
layout: post
title: "[Design] Cache and Page Replacement Algorithms"
comments: true
category: Design

---

### Cache Algorithms

This post is originally written for __Cache Algo__ only, before I found out this 2 topics are very similar, so I changed the title to "Cache and Page Replacement Algorithms". 

#### Equation 

of memory reference time is:

T = m * T(m) + T(h) + E

> m: miss ratio = 1 - hit ratio
>
> T(m): time for main memory access
>
> T(h): latency (when there's a hit)
>
> E: secondary effects liek queuing effects etc. 

#### hit ratio

how often a searched-for item is actually found in the cache

#### latency

how long after requesting a desired item the cache can return that item (when there is a hit). 

### Replacement policy

#### Bélády's Algorithm (Optimal Algorithm)

The optimal algorithm, not implementable in practise. 

#### LFU

Least Frequently Used, slow and not very adaptive. 

#### LRU 

Fast and adaptive, but hard to implement. 

It can be implemented with either a counter or a stack/doubleLinkedList. 

Web browser use this. 

#### LRU2 and 2Qs

__LRU2__ - Only add entries to the cache the second time they are accessed. 

__Two Queues__ - Add entries to an normal LRU cache. If accessed again, move it to second, larger, LRU cache. 

#### MRU (most recent used)

Some claim that MRU cache algorithms have more hits than LRU due to their tendency to retain older data. 

#### FIFO

Low-overhead, fast but not adaptive. 

#### Second-chance

Modified version of FIFO. Relatively better than FIFO at little cost. 

Initially, a reference bit is set. Instead of removing old entries, it clears reference bit first, and insert that entry at the back of the queue. An entry is only cleared if the reference bit is not set. This is like a circular queue. 

If all the pages have been referenced, second chance degenerates into pure FIFO. Why? Let's say all entries reference are set, the pointer will go around the entire list and clear all references, and in the end come back to the starting point. Then, it's like a FIFO. For more, see the [link](http://javalandscape.blogspot.sg/2009/01/cachingcaching-algorithms-and-caching.html). 

#### Clock

Modified version of second-hand. Better than second hand. Instead of pushing to the back, it keep a "hand" pointer in the circular list. [link](http://javalandscape.blogspot.sg/2009/01/cachingcaching-algorithms-and-caching.html)

When cache miss occurs and no empty place exists, then I consult the R (referenced) bit at the hand's location to know what I should do. If R is 0, then I will place the new entry at the "hand" position, otherwise I will clear the R bit. Then, I will increment the hand (iterator) and repeat the process until an entry is replaced.

#### Simple time-based

Fast, but not adaptive. Entries remain in cache for a specific amount of time. 

#### Extended time-based expiration

Only clear cache at certain points in time (say every 5 minutes). 

### Conclusion

Each replacement strategy is a __compromise between hit rate and latency__. 

#### One more thing

What is Distributed cache? 

[Distributed cache](http://en.wikipedia.org/wiki/Distributed_cache) is an extension of the traditional concept of cache used in a single locale. 

A distributed cache may __span multiple servers__ so that it can grow in size and in transactional capacity. It is mainly used to store __application data residing in database and web session data__. 

The idea of distributed caching has become feasible now because main memory has become very cheap and network cards have become very fast (speed of 1 Gbit is now standard, and 10 Gbit is gaining traction). 

Also, a distributed cache works well on __lower cost machines usually employed for web servers__ as opposed to __database servers__ which require expensive hardware.
