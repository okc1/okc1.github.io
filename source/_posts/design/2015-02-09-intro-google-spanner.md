---
layout: post
title: "[Design] Intro to Google Spanner "
comments: true
category: Design

---

### Spanner

[Spanner](http://en.wikipedia.org/wiki/Spanner_%28database%29) is Google's globally __distributed NewSQL database, the successor to BigTable__. Google describes Spanner as not a pure relational system because each table must have a primary-key column. 

Currently, __F1, Google's advertisement platform__, uses Spanner. Gmail and Google Search will also use it soon.

### NewSQL VS. NoSQL

__NewSQL__, a wholly different database architecture, differentiated from NoSQL, is beginning to emerge. 

#### NoSQL

There are many reasons why NoSQL products have been popular. As there are a variety of NoSQL products. As you can see in Hadoop or Cassandra, main advantages of NoSQL is its horizontal scalability. 

As these NoSQL products __don't provide Strong Consistency__, they cannot be used where __high-level data consistency__ is required. 

#### NewSQL

NewSQL has as __excellent scalability__ as NoSQL, and at the same time it __guarantees ACID like RDBMS__ which is performed in a single node. 

### What is Spanner?

Spanner is [a NewSQL created by Google](http://www.cubrid.org/blog/dev-platform/spanner-globally-distributed-database-by-google/). It is a distributed relational database that can distribute and store data in Google's BigTable storage system in multiple data centers. Spanner meets ACID (of course, it supports transaction) and supports SQL. 

__Data R/W eff__: When you read data, Spanner connects you to the data center that is geographically closest to you, and when you write data, it distributes and stores it to multiple data centers. 

__Failure__: If the data center you try to access has a failure, of course, you can read the data from another data center that has a replica of the data (in US, __5 replica__). 

The Spanner client automatically __performs a failover between replicas__. When the number of servers storing data is changed or a failure occurs in equipment, Spanner automatically __re-distributes data__ through data transfer among the equipments.

More details of Spanner: will come later. 
