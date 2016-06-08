---
layout: post
title: "[Java OOP] PubSub (Publish–subscribe) pattern "
comments: true
category: Java OOP

---

### Publish–subscribe pattern

__[The publish–subscribe pattern](http://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern) is a messaging pattern__ where senders of messages, called publishers, do not send messages directly to specific subscribers. Instead, published messages are characterized into classes without knowledge of subscribers. 

Similarly, subscribers express interest in one or more classes, without knowledge of what publishers there are. 

1. greater network scalability
1. a more dynamic network topology
1. decreased flexibility to modify the Publisher and its structure of the data published.

Pub/sub is typically a part of a larger __message-oriented middleware system__. e.g. Java Message Service (JMS). 

### Difference w/ observer pattern

Refer to __[Java OOP] Observer pattern__ or [this link](http://stackoverflow.com/questions/15594905/difference-between-observer-pub-sub-and-data-binding): 

#### Observer, or Observable/Observer:

> A design pattern by which an object is imbued with the ability to notify others of specific events - typically done using actual events, which are kind of like slots in the object with the shape of a specific function/method. The observable is the one who provides notifications, and the observer receives those notifications. In .net, the observable can expose an event and the observer subscribes to that event with an "event handler"shaped hook. No assumptions are made about the specific mechanism which notifications occur, nor about the number of observers one observable can notify.

#### Pub/Sub:

> Another name (perhaps with more "broadcast" semantics) of the Observable/Observer pattern, which usually implies a more "dynamic" flavor - observers can subscribe or unsubscribe to notifications and one observable can "shout out" to multiple observers. In .net, one can use the standard events for this, since events are a form of MulticastDelegate, and so can support delivery of events to multiple subscribers, and also support unsubscription. Pub/sub has a slightly different meaning in certain contexts, usually involving more "anonymity" between event and eventer, which can be facilitated by any number of abstractions, usually involving some "middle man" (such as a message queue) who knows all parties, but the individual parties don't know about each other.
