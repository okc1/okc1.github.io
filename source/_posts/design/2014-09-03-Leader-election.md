---
layout: post
title: "[Design] Leader Election"
comments: true
category: Design

---

### Question 

(this question is from MIT handouts B)

> Describe a technique to identify a "leader" among a group of 10 identical servers that are all connected to every other server. 

> There are no prior distinguishing characteristics of any of them and the same program to identify the leader starts running on all of them at the same time. After an answer is given, ask how much network traffic it requires and, if "ties" are possible, ask how you can break ties.

### Leader Election 

__[Leader Election](http://en.wikipedia.org/wiki/Leader_election)__ is the process of designating a single process as the organizer of some task distributed among several computers. After running this algorithm, each node throughout the network recognizes a unique node as the task leader. 

The good answer would be: 

Have each server wait a random amount of time and then say "I'm it." The "I'm it" __announcement is time‐stamped__, and the computer that __time‐stamped its announcement first__ is elected the leader. 

This approach requires sending out 9 messages. __If there is a tie__, the computers can repeat the procedure.
