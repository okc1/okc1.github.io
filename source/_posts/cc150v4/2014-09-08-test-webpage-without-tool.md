---
layout: post
title: "[CC150v4] 11.4 Test Webpage without Tools "
comments: true
category: CC150v4

---

### Question

> How would you load test a webpage without using any test tools?

### Solution

#### Load testing

__[Load testing](http://en.wikipedia.org/wiki/Load_testing)__ is testing under normal and peak load condition. It's also called software performance testing, reliability testing, and volume testing.

#### Steps

__First identify the performance-critical scenarios__, which might include: 

1. response time
1. throughput
1. resource utilization
1. max load that system can bear

__Then, design tests to simulate the load__: we can create virtual users by a multi-threaded program with 1000 thread, each acting as a user loading the page. We measure response time of each user. 
