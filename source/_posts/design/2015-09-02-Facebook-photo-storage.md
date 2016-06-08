---
layout: post
title: "[Design] Facebook Photo Storage "
comments: true
category: Design

---

# Stats

Facebook has 1.5 billion monthly active users, 970 million daily active users [as of June 2015](http://newsroom.fb.com/company-info/). 

{% img middle /assets/images/facebook-user-count.png %}

image from [statista.com](http://www.statista.com/statistics/264810/number-of-monthly-active-facebook-users-worldwide/). 

In 2009, Facebook stores 15 billion photos for the user, which grows at 220 million per week, and 550,000 per second at peak. 
    
It's 2015 now, you might want to mulitply these numbers by 3~6. 

I have roughly estimated the statistics of Facebook users, Facebook photos and growth rate, just to give you an idea of the size of data Facebook has got: 

> Total user: 1.5b
>
> Total photoes: 150b, which is 100 photo/user
>
> Each photo got 4 different sizes, so 600b photos are stored. 
>
> New photo per day: 500m
>
> New photo per second: 6,000
>
> Peak incoming photo per second: 3m

# Old architecture

3 tiers design:

1. __Upload tier__ receives users’ photo uploads, scales the original images and saves them on the NFS storage tier.

1. __Photo serving tier__ receives HTTP requests for photo images and serves them from the NFS storage tier.

1. __NFS storage tier__ built on top of commercial storage appliances.

> __[Network File System](https://en.wikipedia.org/wiki/Network_File_System)__ (NFS) is a distributed file system protocol originally developed by Sun Microsystems in 1984, allowing a user on a client computer to access files over a network much like local storage is accessed. 

## Problem

1. there is an __enormous amount of metadata__ 

    ... so much that is [exceeds the caching abilities of the NFS storage tier](https://code.facebook.com/posts/685565858139515/needle-in-a-haystack-efficient-storage-of-billions-of-photos/), __ resulting in multiple I/O operations__ per photo upload or read request

## Solution

1. relies heavily on CDNs to serve photos. 

1. Cachr: a caching server tier caching Facebook "profile" images.

1. NFS file handle cache - deployed on the photo serving tier eliminates some of the NFS storage tier metadata overhead

# Haystack Photo Infrastructure 

The new photo infrastructure merges the __photo serving__ and __storage tier__ into one physical tier. It implements __a HTTP based photo server__ which stores photos in a generic object store called Haystack. 

Goal: eliminate any unnecessary metadata overhead for photo read operations, so that each read I/O operation was only reading actual photo data

5 main functional layers:

1. HTTP server

1. Photo Store

1. Haystack Object Store

1. Filesystem

1. Storage

## Storage 

The commodity machine HW typically is 2x quadcore CPU + 32GB RAM + 512MB NV-RAM cache + 12TB SATA drives. 

> [Non-volatile random-access memory](https://en.wikipedia.org/wiki/Non-volatile_random-access_memory) (NVRAM) is random-access memory that retains its information when power is turned off (non-volatile).  
>
> This is in contrast to dynamic random-access memory (DRAM) and static random-access memory (SRAM) 

So each __storage blade__ is around 10TB. Configured as __RAID-6__ partition. 

> [RAID 6](http://searchstorage.techtarget.com/definition/RAID-6-redundant-array-of-independent-disks), also known as double-parity RAID, uses two parity stripes on each disk. It allows for two disk failures within the RAID set before any data is lost.

Pros:

1. adequate redundancy 
1. excellent read performance 
1. low storage cost down 

Cons:

__The poor write performance__ is partially mitigated by the __RAID controller NVRAM write-back cache__. Since the reads are mostly random, the NVRAM cache is fully reserved for writes. 

__The disk caches are disabled__ in order to guarantee data consistency in the event of a crash or a power loss.

## Filesystem 

### How does filesystem read pictures?

Photo read requests result in __read() system calls__ at known offsets in these files.

Each file in the filesystem is represented by a structure called an inode which contains a block map that maps the logical file offset to the physical block offset on the physical volume. 

For large files, the block map can be quite large.

### Problem

__Block based filesystems__ maintain mappings for __each logical block__, and for large files, this information will not typically fit into the cached inode and is stored in indirect address blocks instead, which must be traversed in order to read the data for a file. 

There can be several layers of indirection, so a single read could result in __several I/Os__ (if not cached).

### Solution

__Extent based filesystems__ maintain mappings only for contiguous ranges of blocks (extents). A block map for a contiguous large file could consist of only one extent which would fit in the inode itself. 

> [An extent](https://goo.gl/uQA35V) is a contiguous area of storage reserved for a file in a file system, represented as a range. A file can consist of zero or more extents; __one file fragment requires one extent__. The direct benefit is in storing each range compactly as two numbers, instead of canonically storing every block number in the range.
>
> Extent-based file systems can also __eliminate most of the metadata overhead of large files__ that would traditionally be taken up by the block allocation tree... saving on storage space is pretty slight, but... __the reduction in metadata is significant and reduces exposure to file system corruption__ as one bad sector in the _block allocation tree_ causes much greater data loss than one bad sector in stored data.

### Problem of Extent-based file systems

However, if the file is severely fragmented and its blocks are not contiguous on the underlying volume, its block map can grow large as well. 

### The solution

Fragmentation can be mitigated by __aggressively allocating a large chunk of space__ whenever growing the physical file. 

Currently, the filesystem of choice is XFS, an extent based filesystem providing efficient file preallocation. 

> __[XFS](https://en.wikipedia.org/wiki/XFS)__ is a high-performance 64-bit journaling file system created by Silicon Graphics, Inc (SGI) in 1993.
>
> ...was ported to the Linux kernel in 2001. As of June 2014, XFS is supported by most Linux distributions, some of which use it as the default file system.
>
> XFS enables __extreme scalability of I/O threads__, file system bandwidth, and size of files and of the file system itself when spanning multiple physical storage devices. 
>
> Space allocation is performed via extents with __data structures stored in B+ trees__, improving the overall performance of the file system, especially when handling large files.
>
> __Delayed allocation__ assists in the prevention of file system fragmentation; __online defragmentation__ is also supported. A feature unique to XFS is the __pre-allocation of I/O bandwidth__ at a pre-determined rate, which is suitable for many real-time applications.

## Haystack

Haystack is a simple __log structured (append-only) object store__. Many images store in one Haystack. Typically, [Haystack Store is 100GB size](http://jishu.zol.com.cn/17742.html). 

A Haystack consists of two files:

1. __haystack store file__ (containing the needles)
    1. superblock
    1. needles (1 needle is 1 image)
1. __an index file__

### 1. haystack store file 

{% img middle /assets/images/851582_1409519009260319_311676661_n.jpg %}

1. The first 8KB of the haystack store is occupied by the __superblock__. 

1. following the superblock are __needles__

    __Needles represents the stored objects__. Needle consisting of a header, the data, and a footer: 

    {% img middle /assets/images/851578_319395058204993_541487263_n.jpg %}

    A needle is uniquely identified by its \<Offset, Key, Alternate Key, Cookie\> tuple. 

    Haystack doesn’t put any restriction on the values of the keys, and there can be needles with duplicate keys. 

### 2. Index File

__Needle__ consisting of a header, the data, and a footer: 

{% img middle /assets/images/851582_1374324519464800_699636937_n.jpg %}

The index file provides the minimal metadata required to locate a particular needle in the haystack store file. 

{% img middle /assets/images/851582_314454922033518_1196942525_n.jpg %}

The index file is not critical, as it can be rebuilt from the haystack store file if required. 

The main purpose of the index: quick loading of the needle metadata into memory without traversing the larger Haystack store file, since the index is usually less than 1% the size of the store file. 

### Summary

All needles are stored in Haystack store file, and their location information is stored in Index File. 

What is Needle? Needles represents the stored objects (1 needle - 1 image). 

## Haystack Operations

1. __write__

    append new needle to haystack store file.
    
    later, corresponding index records are __updated async__. 
    
    In case of failure, any partial needles are discarded, and fix index from the end of the haystack.
    
    You can't overwrite any needle, but you can insert using same key. Later, the needle __with dup keys but largest offset__ became the most recent one. 

1. __read__

    __parameters passed in__: offset, key, alt key, cookie, data size
    
    if key, alt key and cookie matches, and checksum correct and needle is not marked as deleted, return. 

1. __delete__

    marks needle as deleted (set 1 bit), but index is not modified. 
    
    the deleted space is not reclaimed unless __compact the haystack__

## Photo Store Server 

Photo Store Server is responsible for accepting HTTP requests and translating them to the corresponding Haystack store operations. 

In order to minimize the number of I/Os required to retrieve photos, the server keeps an __in-memory index of all photo offsets__. 

At startup, __the (photo) server reads the haystack index file and populates the in-memory index__. The in-memory index is different from the index file in Haystack, as it stores lesser information, like this: 

{% img middle /assets/images/851584_503528913060377_1268325854_n.jpg %}

1. __Photo Store Write/Modify Operation__

    1. writes photos to the haystack 
    1. updates the in-memory index 
    
    if there are duplicate images, the one stored at a larger offset is valid.

1. __Photo Store Read Operation__

    passed in:
    
    1. haystack id 
    1. a photo key, 
    1. size 
    1. cookie 
    
    The server performs a lookup in the in-memory index based on the photo key and retrieves the offset of the needle containing the requested image.
    
    Since haystack delete operation doesn’t update the haystack index file record. Therefore a freshly populated in-memory index can contain stale entries for the previously deleted photos. Read such photo will fail and the in-memory index is updated to 0.

1. __Photo Store Delete Operation__

    After calling the haystack delete operation, the in-memory index is updated to 'offset = zero' 

1. __Compaction__

    Compaction is an online operation which reclaims the space used by the deleted and duplicate needles.
    
    creates a new haystack 

1. __HTTP Server__

    evhttp server 

    multiple threads, with each serving a single HTTP request. Workload is mostly I/O bound, thus the performance of the HTTP server is not critical.

# Summary 

Storing photos as needles in the haystack __eliminates the metadata overhead__ by aggregating hundreds of thousands of images in a single haystack store file. 

This keeps the metadata overhead very small and allows us to __store each needle’s location in the store file in an in-memory index__. 

This allows retrieval of an image’s data in __a minimal number of I/O operations__, eliminating all unnecessary metadata overhead. 

Ref: https://code.facebook.com/posts/685565858139515/needle-in-a-haystack-efficient-storage-of-billions-of-photos/
