---
layout: post
title: "[NineChap System Design] Class 1.1: Overview "
comments: true
category: NineChap

---

# Overview

## defination 

the process of defining the __architecture, components, modules, interfaces and data__ to satisfy specified __requirements__. 

1. conceptual design (macro)
2. logical design
3. physical design (micro)

### Top-down design

Eg. MS Office, Huawei Security System

### Bottom-up design

Most start-up use, MVP first using Medetor + MongoDb. 

## 5 steps (SNAKE Principle):

1. __Scenario__: case/interface - input
1. __Necessary__: constrain/hypothesis - input
1. __Application__: service/algorithm - output
1. __Kilobit__: data - output
1. __Evolve__ - solution

# A top-down example

Example one: __design a radio__

## Step One, Scenario

1. brain storm

    1. register/log in
    1. play music
    1. recommendation

1. prioritize

    1. play music
        1. Get channel
        1. select a channel
        1. play

## Step Two, Necessary

1. ask

    1. total user - 100,000,000
    1. __daily users - 1,000,000__

1. predict

    1. user analysis
    1. Traffic analysis
    1. Memory analysis
    1. QPS

Details:

1. user analysis

    > Avg Concurrent users = daily users __/ 5__ = 200,000
    >
    > Peak Concurrent users = concurrent user __\* 3__ = 600,000

    considering your product may grow in the next 3 month:
    
    > Max Peak users in 3 month = Peak users __\* 10__ = 6,000,000

1. Traffic analysis

	> Request of new music per user: 1 music/min
	>
	> Music size = 3MB
	>
	> Max peak traffic (in 3 months) = 6,000,000 \* 3MB / 60 = 300GB/s

1. Memory analysis

	> Memory per user (metadata) = 10KB
	>
	> Max daily memory = 1,000,000 \* 10 \* 10 = 100 million KB = 100GB
    >
    > (10 times of avg daily user)

## Step Three, Application

1. Replay the case, one service for each
1. Merge the services

{% img middle /assets/images/design-class1-basic-receptionist.png %}

## Step Four, Kilobit: data

1. Append 1 dataset for each service

    Eg. User service: stability, more addition, less modify and deletion.

    Eg. Channel Service: high concurrency, MongoDB

    Eg. Music Service: MP3 File Systems

{% img middle /assets/images/design-class1-reco-5.png %}

## Last Step, Evolve

1. Better: constrains 

    eg. able to handle 300GB/s traffic?

1. Broader: new cases

    share music? delete user account?

1. Deeper: details design

From views of __Performance, Scalability and Robustness__.

{% img middle /assets/images/design-class1-snake.jpg %}
