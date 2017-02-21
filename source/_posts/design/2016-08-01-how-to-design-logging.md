---
layout: post
title: "[Design] How to Design Logging"
comments: true
category: Design

---

# Logging

Conecting between __information__ and __knowledge__. 

1. Information: it's just bits
2. __Knowledge__: drives product direction

## Logging is all about Event

Q1. shall we log it live? what should we log? how to do it (on different platforms)?

Not live. Do it asynchronously.

__Demand and product design__ drives logging. 

Logs represent event, so all your logging should be __based around the events__.

> eg. who click the button, the user ID, but do not log the age, because you can find it somewhere else!

## Think about "what" to log and "why"

__"How" is just coding__. Happy Logging! 
