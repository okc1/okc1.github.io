---
layout: post
title: "[NineChap System Design] Class 3.2: Web Service "
comments: true
category: NineChap

---

# Question 4

__fix MP3 problem__

The process of fetching a MP3 (from CDN):

{% img middle /assets/images/design-class3-client-request-mp3.png %}

1. aquire MP3 link, and send request
1. send request to CDN
1. CDN receive request, find MP3
1. response to client
1. play the music

{% img middle /assets/images/design-class3-client-request-mp3-errors.png %}

Question: in step 2, there's more Network error, but in step 4, there's no Network error, but Timeout. Why?

## Fix step 2, Network error

Problem is: MP3 url invalid. It actually comes from a failed CDN sever. 

Solution: fix the server.

## Fix step 3, CDN can't find MP3 

Problem associated with __Anti-Leech__. 

> __[a leech](https://en.wikipedia.org/wiki/Leech_(computing))__ is one who benefits, usually deliberately, from others' information or effort but does not offer anything in return. 
>
> Example: Wi-Fi leeches, Direct linking (or hot-linking) and In most P2P-networks, leeching is whose who download too much.

> __[Anti-Leech](https://answers.yahoo.com/question/index?qid=1006042926419)__ specializes in protecting file downloads and stopping bandwidth leeching. 

See that some P2P and leeching software will steal your url links, so the MP3 url expiration time is 5 minutes. 

So when CDN server's clock and web server's clock are not synchronized well, MP3 url can expire. 

Solution: every 10 minutes sync CDN clock with web server clock. 

## Fix step 4, Timeout error

Some MP3 are relatively large. Thus timeout. 

> MP3 performs better at higher bps, and aac(Advanced Audio Coding) works better at lower bps. 

Solution: 

1. compress MP3 to 48bps, or use aac format. So, play lower-rate music first, then switch automatically.

1. pre-load a music while previous is playing. 

1. optimize CDN

> __[CDN](https://en.wikipedia.org/wiki/Content_delivery_network)__ content delivery network is a large __distributed system of servers__ deployed in __multiple data centers__ across the Internet. 

> The goal of a CDN is to serve content to end-users with high availability and high performance.  

{% img middle /assets/images/design-class3-CDN.png %}

Which CDN should client choose?

> Not DNS, but web server calculates which to choose. It can be calculated using IP distance, or ISP provider, but not accurate. 

> We can also use local desktop apps (in different locations) to ping CDN servers. This may violate user privacy, though. 

## Fix step 5, Fail to play

Problem: some files got wrong decoding. 

## Fix step 6, unkown error

Problem: some users close the page while MP3 loading. 

# Question 5

__fix player problem__

Problem: iOS device can never play Flash. 

Solution: develop HTML5 player. 

## 5.2 how to evaluate that you solved the problem

1. user complains

1. __important__: daily retention rate! 

We can't use daily active user, cuz it depends on marketing, competitors, and infrastructure changes. 

__One day retention rate__:

{% img middle /assets/images/design-class3-user-retention.png %}

> Today’s visitor = {U1, U3, U7, U9, U10} 
>
> Tomorrow's visitor = {U2, U3, U9,}
>
> Today’s one day retention rate = 2/5

# Question 6 秒杀

## Design

Queue A and Queue B

{% img middle /assets/images/design-class3-miao-sha.png %}

### Queue A

Many queues, each one locates on a individual web server or reverse proxy. It is mainly used to accept large amount of requests coming from the clients. 

Each machine may takes 10,000 or more requests per second. 

Queue A will redirect most requests to a static page (cached).

### Queue B

Queue B is a single machine, to aviod distributed problems. It takes in small amount of requests and decides results (eg. redirect to payment page). 

> Now, why do we need 2 queues, not 1?

> Think about a hospital. Queue A is the hospital lobby and security guard, and Queue B is the queue of patience. 

## How to reduce traffic

1. no image
1. cache more static pages
1. reverse proxy: batch sending the requests

Also, can use front-end javascript to prevent clicking. There are method to bypass, so we need to check IP or do some filtering. 

## How to keep it simple?

1. no DB: basic logic. But rmb to use a log file
1. no lock

## How to improve stability

1. use new server to do __Miao Sha__, in case of crash
1. asyc prcessing everything! Don't let other people wait, in case of crash. 

### How to defend hackers

1. IP address (to defent auto softwares), but it's easy for hackers to fake IP address
1. CAPTCHA 

> __[CAPTCHA](https://en.wikipedia.org/wiki/CAPTCHA)__ (an acronym for "Completely Automated Public Turing test to tell Computers and Humans Apart") is a type of challenge-response test used in computing to determine whether or not the user is human. 

## follow-up

How to design 12306 (support several million QPS)
