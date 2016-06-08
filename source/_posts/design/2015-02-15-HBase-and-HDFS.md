---
layout: post
title: "[Design] HBase and HDFS"
comments: true
category: Design

---

### Overview 

[Hadoop Distributed File System](http://hortonworks.com/hadoop/hdfs/) (HDFS) is a __Java-based file system__ that provides scalable and reliable data storage that is designed to span large clusters of commodity servers. __HDFS, MapReduce__, and YARN form the core of Apache™ Hadoop®.

[Apache HBase](http://hbase.apache.org/) is the Hadoop database, a distributed, scalable, big data store.

#### Hadoop

Hadoop is [basically 2 things](http://stackoverflow.com/a/16930049), a FS (Hadoop Distributed File System) and a computation framework (MapReduce). 

HDFS allows you store huge amounts of data in a distributed (provides faster read/write access) and redundant (provides better availability) manner. And MapReduce allows you to process this huge data in a distributed and parallel manner. 

But MapReduce is not limited to just HDFS. 

#### HDFS and HBase

Being a FS, HDFS lacks the random read/write capability. It is good for sequential data access. And this is where HBase comes into picture. It is a NoSQL database that runs on top your Hadoop cluster and provides you random real-time read/write access to your data.

### Now, the Comparison

__HDFS is a distributed file system__. [ref](http://qr.ae/BqrVU)

1. It is optimized for streaming access of large files. You would typically store files that are in the 100s of MB upwards on HDFS and access them through MapReduce to process them in batch mode. 
2. HDFS files are write once files. You can append to files in some of the recent versions but that is not a feature that is very commonly used. Consider HDFS files as write-once and read-many files. There is no concept of random writes.
3. HDFS doesn't do random reads very well.

__HBase is a database that stores it's data in a distributed filesystem__. 

The filesystem of choice typically is HDFS owing to the tight integration between HBase and HDFS. It doesn't mean that HBase can't work on any other filesystem.

1. Low latency access to small amounts of data from within a large data set. You can access single rows quickly from a billion row table.
2. Flexible data model to work with and data is indexed by the row key.
3. Fast scans across tables.
4. Scale in terms of writes as well as total volume of data.
