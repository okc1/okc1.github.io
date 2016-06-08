---
layout: post
title: "[NineChap System Design] Class 1.3: Improvement "
comments: true
category: NineChap

---

# From Level 0 to Level 1

Refer to the previous question. How can we improve???

1. performance
1. scalability
1. robustness

## performance

A better algo: Inverted Index

{% img middle /assets/images/design-class1-reco-2.png %}

Avg performance increase to ~ 20ns (with some optimization of MapReduce procedure, discuss later). 

__Max QPS increase to 50__. 

## scalability

Use a __dispatcher__ to re-direct the requests to multiple machines. 

{% img middle /assets/images/design-class1-reco-3.png %}

### How many machines do we need then? 

Well we need 500 QPS. The algo above achieves ~ 50 QPS. __Should we need 10 machines__?

The answer is NO. A machine with 8 (or 16) core CPU could be able to handle. 

We can also have a __hot-standby__, to be safe. 

> hot standby is used as a failover mechanism to provide reliability in system configurations. 
>
> When a key component fails, the hot spare is switched into operation. 

## robustness

Tips about system design for senior engineers: 

> __Draw 1 machine first__. This machine can contains multiple datasets and run multiple processes. 
>
> On top of this machine, the interface layer is __one single Manager process__. The Manager is in charge of almost everything: handling data lost, handle high concurrency, copy multiple instance of itself... 
>
> Like this: 

{% img middle /assets/images/design-class1-reco-6.png %}

### Back-end

Now we need __a cluster of datasets__ (which has Manager on top of it), and __a cluster of Recommenders__. Manager is in charge of copying multiple instances. 

Dataset can be put in different physical locations. Recommender don't really need, cuz it's only do calculation job. 

### Receiving requests

Just now we used __Receptionist (or Dispatcher)__ to handle request. Now we use a __Web service__ (eg. Apache). It's not necessary to make it a cluster. 

### Big Brother

We need a __monitor system__ to oversee everything. 

Also, Big Brother is in charge of heart-beat. If not received, Big Brother have some double-check machanism. 

{% img middle /assets/images/design-class1-reco-4.png %}

### Connecting the dots

__Dispatcher__ is used to connect the 4 components. It's like a messaging queue that collects and distributes jobs among everybody (eg. control and distributed info). 

It can be stateful or stateless. 

Keep in mind __the connection between Dataset and Recommender__ remains. It's slow going thru Dispatcher. 

### Distribute it

During development, the 5 components can be put on same machine. When we deploy distributely, we use __Socket connection (keep alive)__ to connect them. 

Notice the Web Service is __connection heavy__, which consume large CPU and RAM resource. It's better to seperate to one machine. 

Big brother is read/write heavy, so it's OKAY to put on same machine with Dispatcher. 

Since Dataset and Recommender have data exchange, it's a good idea to put on same machine. 

### Additional questions

Implement Dispatcher with __consumer-producer__ model. 
