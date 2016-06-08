---
layout: post
title: "[Java OOP] BlockingQueue and Thread Pool "
comments: true
category: Java OOP
tags: [ src ]
---

### Blocking Queue VS. Thread Pool

These are 2 very different things, however it might be a little bit confusing for a layman. I have very little knowledge about Java multi-threading. But after writing some example of thread pool and blockingqueue, I am able to identify some significant differences between the 2 DS: 

1. Thread pools are often used in multi threaded servers. For example, we create 10 thread only for processing 1,000 tasks. However in BlockingQueue, there're typically only 2 thread: Producer and Consumer. Of course there can be more, but the basic pattern defines only 2 (types of) threads. 

1. Threads are added into thread pool, while in BlockingQueue, it stores tasks (runnables). 

It's not a common practise to compare the 2 DS. If you read this and have got some interesting thoughts, do not hesitate to let me know by commenting below! 
