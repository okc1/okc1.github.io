---
layout: post
title: "[Design] Amazon Web Services"
comments: true
category: Design

---

## Overview

__[Amazon Web Services](http://en.wikipedia.org/wiki/Amazon_Web_Services)__ (AWS) is a collection of __remote computing services__ that together make up a cloud computing platform. AWS provides a large computing capacity much faster and cheaper than building a physical server farm. 

The most well-known is Amazon EC2 and Amazon S3. 

[Amazon is an example of](http://practicalcloudcomputing.com/post/311045887/cloudexplained) an __IAAS (Infrastructure as a Service) provider__. 

### Terminologies

#### AWS

Amazon Web Services, a division of Amazon focusing on hosting our applications and data

#### SimpleDB

AWS’s always-available replacement for RDBMSs. Specifically SimpleDB is their hosted, replicated key-value store that is always available and accessible as a web service

#### S3

(a.k.a Simple Storage Service) AWS’s always-available file storage solution accessible as a web service

#### SQS

(a.k.a Simple Queue Service) AWS’s always-available queueing service accessible as a web service

#### ELB

(a.k.a Elastic Load Balancer) AWS’s always-available load balancing service accessible as a web service

#### EC2

(a.k.a Elastic Compute Cloud) AWS’s on-demand server offering accessible as a web service

#### CloudFront

AWS’s CDN (a.k.a Content Delivery Network) offering accessible as a web service

### Benefits

Basically, by moving these services out of your data center and into the cloud, you:

1. __No longer need to run and maintain a data center__. You no longer need the associated staff

1. Get a __more scalable and available infrastructure__ without trying to build it yourself
