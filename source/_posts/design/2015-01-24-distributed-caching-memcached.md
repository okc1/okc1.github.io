---
layout: post
title: "[Design] Distributed Caching - memcached "
comments: true
category: Design

---

### What is Memcached?

[Memcached](http://memcached.org/) is an __in-memory key-value store for small chunks of arbitrary data__ (strings, objects) from results of database calls, API calls, or page rendering.

1. Free & open source
1. high-performance, distributed memory object caching system
1. generic in nature
1. intended for use in speeding up dynamic web applications by alleviating database load

Definition from [wiki](http://en.wikipedia.org/wiki/Memcached): 

> Memcached is a __general-purpose distributed memory caching system__. It is often used to speed up dynamic database-driven websites by __caching data and objects in RAM__ to reduce the number of times an __external data source__ (such as a database or API) must be read.

### Who uses Memcached?

1. Facebook
1. YouTube
1. Twitter
1. Amazon
1. Reddit
1. Yahoo
1. Zynga

### Why Memcached?

Run memcached on one or more hosts and then use the shared cache to store objects. Because each host’s RAM is storing information, the access speed [will be much faster than](http://www.blogs.zeenor.com/category/interview-questions/page/9) having to load the information from disk. This can provide __a significant performance boost in retrieving data__ versus loading the data natively from a database. 

Also, because the cache is just a repository for information, you can use the cache to store __any data, including complex structures__ that would normally require a significant amount of effort to create, but in __a ready-to-use format__, helping to reduce the load on your MySQL servers. 

### FAQ

__What is Memcached?__

[It is component](http://www.web-technology-experts-notes.in/2014/09/memcached-interview-questions-and-answers.html) which stored the data temporary for 1 Hour/ 6 Hour/1 Day etc. When we integrate the Memcached with our application, performance of application increased.

Memcached is open source, high-performance distributed memory object used for caching so that execution can be enhanced at nth level.

__Where Memcached can be used?__

•  Social Networking -> Profile Caching

•  Content Aggregation -> HTML/ Page Caching

•  Ad targeting -> Cookie/profile tracking

•  Relationship -> Session caching

•  E-commerce -> Session and HTML caching

•  Location-based services -> Data-base query scaling

•  Gaming and entertainment -> Session caching

__Why use Memcached?__

•  Speed up application processes

•  It determines what to store and what not to

•  Reduce the number of retrieval requests to the database

•  Cuts down the I/O ( Input/Output) access (hard disk)

__In what condition does retrieving cache fail?__

•  Memory allocated for the cache is exhausted

•  Item from cache is deleted

•  Individual item in the cache is expired

__What is the drawback of Memcached?__
 
•  It is not a persistent data store

•  Not a database

•  It is not an application specific

•  It cannot cache large object

__Give more details about memcached failures__

[Memcached servers](http://programmers.stackexchange.com/a/187101) are indeed independent of each other. Memcached server is just an efficient key-value store implemented as in-memory hash table. 

__What makes memcached distributed is the client__, which in most implementations can connect to a pool of servers. Typical implementations use consistent hashing, which means that when you add or remove server to/from a pool of N servers, you only have to remap 1/N keys. 

Typically keys are __not duplicated__ on various hosts, as memcached is __not meant to be persistent store__ and gives no guarantees that your value will persist (for example when running out of assigned memory, memcached server drops least recently used (LRU) elements). Thus it's assumed that your application should handle missing keys.
