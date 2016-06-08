---
layout: post
title: "[Design] Cloud, Grid and Cluster "
comments: true
category: Design

---

[ref](http://stackoverflow.com/questions/9723040/what-is-the-difference-between-cloud-grid-and-cluster)

### Cluster VS. Grid

__[Cluster differs](http://stackoverflow.com/a/9753568) from Cloud and Grid in that__ 

1. a cluster is a group of computers connected by a local area network (LAN)
1. cloud and grid are more wide scale and can be geographically distributed. 

Another way to put it is to say that

1. a cluster is tightly coupled
1. a Grid or a cloud is loosely coupled. 

Also, __the hardware__: 

1. clusters are made up of machines with similar hardware
1. clouds and grids are made up of machines with possibly very different hardware configurations. 

### Computer cluster

__[A computer cluster](http://en.wikipedia.org/wiki/Computer_cluster)__ consists of a set of tightly connected computers that work together as a single system. 

Unlike grid computers, computer clusters have each node set to __perform the same task__, controlled and scheduled by software. 

In most circumstances, all of the nodes use the __same hardware and OS__. They are connected in __LAN__ with each node running its __own piece__ of OS. 

They are used to improve __performance__ and __availability__ over that of a single computer, while being more __cost effective__. 

Computer clusters emerged as a result of: 

1. low-cost microprocessors, 
1. high-speed networks, 
1. software for high-performance distributed computing

### Grid computing

__[Grid computing](http://en.wikipedia.org/wiki/Grid_computing)__ is the collection of computer resources from multiple locations to reach a common goal. Each computer have __non-interactive workloads__. It's like a __"super virtual computer”__ composed of many networked loosely coupled computers acting together to perform large tasks. 

Unlike conventional high performance computing systems such as __cluster computing__, grid computers have each node set to __perform a different task__. 

Grid computers also tend to be more __geographically dispersed__ than cluster computers. Grids are often constructed with general-purpose grid middleware software libraries. 

Major disadvantage with Grid Computing is, __if one piece of software on a node fails__, other pieces of the software on the other nodes may fail. 

### Cloud computing

__[Cloud computing](http://en.wikipedia.org/wiki/Cloud_computing)__ is terminology based on utility and __consumption of computing resources__. 

#### SaaS

An application doesn't access resources it requires directly, rather it accesses them through __something [like a service](http://stackoverflow.com/a/1068133)__. Instead of talking to a specific hard drive for storage, and a specific CPU for computation, etc, it talks to some __service that provides these resources__. The service then maps any requests for resources to its physical resources. 

The services themselves [have long been referred to](http://stackoverflow.com/a/9753568) as __Software as a Service (SaaS)__. The datacenter hardware and software is what we call __a Cloud__. When a Cloud is made available in a pay-as-you-go manner to the general public, we call it a __Public Cloud__; the service being sold is __Utility Computing__. 

#### Sharing of Resources

Usually the service __dynamically allocate resources__ to maximize the effectiveness of the shared resources(per users and per demand). 

For example, a cloud computer facility that serves European users during European business hours with a specific application (e.g., email) may reallocate the same resources to serve North American users during North America's business hours with a different application (e.g., a web server). 

With cloud computing, multiple users can access a single server to retrieve and update their data __without purchasing licenses for different applications__.

#### Scalability

1. If an application requires only __a small amount of some resource__, say computation, then the service only allocates a small amount, say a small share on a single physical CPU. 

1. If the application requires __a large amount of some resource__, then the service allocates that large amount, say a grid of CPUs. 

All the complex handling and coordination is performed __by the service, not the application__. In this way the application can scale well. 

[For example](http://stackoverflow.com/a/1068133) a web site written "on the cloud" may share a server with many other web sites while it has a low amount of traffic. If it ever has massive amounts of traffic, it may be moved to its own dedicated server, or __grid of servers__. This is all handled __by the cloud service (provider)__, so the application shouldn't have to be modified drastically to cope.

#### Other Advantages

Using Cloud Computing, companies can [scale upto High capacities](http://www.ibeehosting.com/blog/what-is-the-difference-between-cloud-computing-and-grid-computing.html) immediately without investing in new infrastructure, training the people or new software licensing. It is more useful for small and medium scale businesses who wants to outsource their Data Center infrastructure, or some larger companies also prefer if they want to cut down the costs of building data-centers internally in order to get peak load capacity. In short, consumers use what they need and pay accordingly.

### Grid Computing VS. Cloud Computing

1. Grid Computing is the parent of Cloud computing, cloud actually evolves from Grid Computing. 

1. A cloud would usually use a grid. A grid is not necessarily a cloud. 

1. Resource distribution: Cloud computing is a centralized model whereas grid computing is a decentralized model where the computation could occur over many administrative domains.

1. Ownership: A grid is a collection of computers which is owned by multiple parties in multiple locations and connected together so that users can share the combined power of resources. Whereas a cloud is a collection of computers usually owned by a single party.

#### Examples

Examples of Clouds: Amazon Web Services (AWS), Google App Engine, Dropbox, Gmail, Facebook, Youtube, Rapidshare

Examples of Grids: FutureGrid
