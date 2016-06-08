---
layout: post
title: "[NineChap System Design] Class 1.2: An Example "
comments: true
category: NineChap

---

# A bottom-up example

Example two: __design a recommendation module__

## A simple algo: 

    u1={m3,m5,m7,m11}
    u2={m1,m2,m3,m4,m5,m6,m7,m8,m9}
    Similarity( u1, u2 ) = 3
    
m - music

u - user

Similarity = # of same music for different users

## Adv algo: 

find his __top-1 similar user__. Stay tuned for future posts. 

## Use the 5 Steps (SNAKE)

1. Step One, Scenario
1. Step Two, Necessary
1. Step Three, Application
1. Step Four, Kilobit: data
1. Last Step, Evolve

Because this question is relatively easy, we will not do case-analysis (Macro). 

__Instead, we do micro design__ by starting at the interface. 

## Step One, Scenario

Interface 

    class Recommender {
        public int findSimilarUser(int userId) {
            //
        }
    }

## Step Two, Necessary

1. ask
    1. total users = 100,000,000
    1. total music = 10,000,000
    1. peak users in 3 month = 6,000,000
    
    However, not everyone is logged in. Thus we won't need to recommend for everybody. On average, the logged-in ratio is 1% - 30%. Let's assume 5%. 
    
    1. participation percentage = 5%
    
    And user's interest won't change every minute. Let's recalculate only after 10 minutes.
    
    1. calculation frequency = 1 update/10min/user

1. predict

    1. user analysis (skip)
    1. Traffic analysis (skip)
    1. Memory analysis (skip)
    1. QPS
    
    Peak QPS = 6,000,000 \* 5% / (10 \* 60) = 500/s

## Step Three, Application

__The simpliest algorithm: BF compare__. The complexity is O(m n) for each user, where m is # of music a person likes, and n is # of total users. For k users, it takes O(k m n) time (k can be = peak concurrent users). 

This is roughly 0.2s per user. Thus __Max QPS = 5__. 

> One word about complexity-to-seconds estimation. 
>
> O(n ^ 3) -> 1s
>
> O(n ^ 2) -> 0.2s
>
> O(n) -> 20ms
>
> O(k) -> k ms

## Step Four, Kilobit: data

Very simple:

{% img middle /assets/images/design-class1-reco-1.png %}

## Last Step, Evolve

Read on. 
