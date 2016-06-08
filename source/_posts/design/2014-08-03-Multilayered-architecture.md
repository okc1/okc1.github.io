---
layout: post
title: "[Design] Multilayered architecture"
comments: true
category: Design

---

### First Word

A [multilayered software architecture](http://en.wikipedia.org/wiki/Multilayered_architecture) is a software architecture that uses many layers for allocating the different responsibilities of a software product.

### Layers

1. __Presentation layer__
    a. UI layer, view layer
    a. presentation tier in multitier architecture
1. __Application layer__
    a. also called service layer/GRASP Controller Layer
1. __Business layer__
    a. also called business logic layer/domain layer
1. Infrastructure layer
    1. data access layer/__persistence layer__
    1. logging, networking, and other services which are required to support a particular business layer

### Conventions

__Application layer__ (or service layer) is sometimes considered a sublayer of __business layer__. 

If there's no explicit distinction between first 3 tiers, then it's a __traditional client-server(two-tier) model__.

The __application/business layers__ can, in fact, be further subdivided to emphasize distinct responsibility (eg. MVC). 

Sometimes there's __business infrastructure layer(BI)__, located between the business layer and infrastructure layer. 

Infrastructure layer can be partitioned into different levels (high-level or low-level). __Developers focus on only the persistence capabilities__, therefore only talk about persistence layer or data access layer. 
