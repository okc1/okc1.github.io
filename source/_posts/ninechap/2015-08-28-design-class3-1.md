---
layout: post
title: "[NineChap System Design] Class 3.1: Web Service "
comments: true
category: NineChap

---

# Overview

Today we'll look at 6 examples of problems associated with Web Service:

1. how the internet works
1. DNS
1. Web server
1. Music Player
1. MP3 file
1. 秒杀

# Question 0

__how to solve raido-play failures__

    > Failure rate  = % user who can't listen to music properly

    > = # user who fail to plya one song / # total users
    
Misson: reduce failure rate.

## How does server identify a user?

{% img middle /assets/images/design-class3-http-request-overview.png %}

> If a server uses __Cookie__ to identify unique users, the result might be > real users.

> However, if server uses __IP address__, the result might be < real users. 

## How to collect data for failure rate

### Version 1

Log: 

1. user send a log to server when it visits
1. user send another log after it plays a song
1. we can identify users who failed to play a song

{% img middle /assets/images/design-class3-server-failure-rate-1.png %}

> In fact, everything should be logged, including play, pause, switch song, refresh etc.

### Version 2

User login are, in fact, __automatically logged__ when user visits. Thus user ONLY have to send log __after it plays music__. 

## Summary

1. define failure rate
1. user cookie to identify user
1. use log to collect failure data
1. analysis pattern of failure againt date/time

# Question 1

__the process of playing music__

{% img middle /assets/images/design-class3-web-browser-17-steps.png %}

1. Prepare
2. Send DNS request
3. Prepare DNS reply
4. Send DNS reply
5. Process DNS reply

    -
    
6. Send webpage request
7. Prepare webpage reply
8. Send webpage reply
9. Process webpage
    
    -
    
10. Request music player
11. Prepare music player
12. Send music player
13. Process music player
    
    -
    
14. Request MP3 
15. Prepare MP3 
16. Send MP3 
17. Play MP3

What is process Music Play?

> Local browser will do rendering, flash decoding etc. If any point of this 17 steps went wrong, the music-play fails. 

Is there a system/browser default Music Play?

> HTML player is, but flash player is not. So the flash module have to be requested every time. 

## Real data: failure rate 20%

In practise, the real failure rate is 20%. Which is:

1. 8% DNS
1. 5% Web
1. 5% MP3
1. 2% Player

# Question 2

__fix DNS problem__

First of all, how to find out DNS failures? There are 2 ways. First way, help desk do it. Second way is to use the Desktop app to help detect the host address. 

## Step 1. HOSTs hijack

Some users' host file can modified by competitors. 

1. ping the website url
1. modify host file manually or by desktop app

## Step 2. ISP

Each ISP have different DNS service. Eg. CSTNET fails to update the latest DNS, after a server change. 

After this step, DNS failure rate fall from 8% to 1%. Why still 1%? Some companies bans music play in company web. 

# Question 3

__fix the web problem__

Highest failure rate:

1. 3pm office hour
1. 9pm highest bandwidth nation-wide

{% img middle /assets/images/design-class3-web-failure-graph.png %}

## Solution 1, reverse proxy

Reverse proxy w/ more servers. Reverse proxy acts like a load balancer. 

{% img middle /assets/images/design-class3-reverse-proxly.png %}

> __[Reverse proxy](https://en.wikipedia.org/wiki/Reverse_proxy)__ is a type of proxy server that retrieves resources on behalf of a client from one or more servers. These resources are then returned to the client as though they originated from the proxy server itself. 

[Common uses for a reverse proxy server](https://www.nginx.com/resources/glossary/reverse-proxy-server/) include:

> 1. Load balancing 

>    act as a “traffic cop,” sitting in front of your back-end servers and client requests. Try to __maximizes speed and capacity utilization__ while ensuring __no one server is overloaded__. 
    
>    If a server goes down, the load balancer redirects traffic to the remaining online servers.

> 1. Web acceleration 

>     can compress inbound and outbound data, as well as __cache commonly requested content__
    
>     also perform additional tasks such as SSL encryption to take __load off of your web servers__

> 1. Security and anonymity 

>     By intercepting requests headed for your back-end servers, a reverse proxy server protects their identities and acts as an additional defense against security attacks. 

## Solution 2, reduce size of web page

1. simplify javascript files
1. compress images (lower dpi)
1. merge large images to 1 image (less requests)
1. lazy loading (Pinterest uses it a lot)

## Solution 3, more cacheable pages

 __Change dynamic webpages to static pages__. The advantage of this is:

1. more search engine friendly.
1. more cache friendly.

### Summary on caching

Caching can happen at place Number 1, 2 and 3:

{% img middle /assets/images/design-class3-web-hosting-4-layers.png %}

AT Number 4, we can add __more servers__. Number 3, __reverse proxy__. Number 2 is __caching within the ISP network__, which avoids requesting info again from backend. Number 1 is __front-end browser cache__. 

After this step, Web failure rate fall from 7% to 4%. Why still 4%? Well, these failure is mainly from the junk users created by marketing.
