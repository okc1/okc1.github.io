---
layout: post
title: "[Design] Multithreading Q&A"
comments: true
category: Design

---

## General Q & A

[source](http://www.geeksforgeeks.org/mutex-vs-semaphore/)

#### Can a thread acquire more than one lock (Mutex)?

Yes, if they need more resource.

#### Can a mutex be locked more than once?

Unless it's a recursive mutex, no. 

A mutex is a lock. 

#### What happens if a non-recursive mutex is locked more than once?

Deadlock. 

Trying to lock the mutex again, it will enter into the waiting queue. But no other thread can unlock that mutex.

#### Are binary semaphore and mutex same?

No. One is __signalling__, another is __locking mechanism__.

A semaphore is [more general concept](http://stackoverflow.com/a/2350628) than mutex. A mutex is (almost) a special case of a semaphore.

#### Why use mutex and critical section?

Critical section is group of instructions that need to be executed atomically. 

The objective of mutex is atomic access of critical section. 

#### Can we acquire mutex/semaphore in an Interrupt Service Routine?

Yes, but very bad practise.

The ISR are meant be short, the call to mutex/semaphore may block the current running thread. However, an ISR can signal a semaphore or unlock a mutex. 

#### What is thread blocking on mutex/semaphore?

When the resource is not available, the requesting thread will be moved from the running list of processor to the waiting list of the synchronization primitive. 

When the resource is available, the higher priority thread on the waiting list will get resource (more precisely, it depends on the scheduling policies).

#### Is it necessary that a thread must block when resource is not available?

No. 

If the design is sure ‘what has to be done when resource is not available‘, the thread can take up that work (a different code branch). To support, application requirements the OS provides non-blocking API.

## Google interview questions

[source](http://www.chiefdelphi.com/forums/showthread.php?p=983786)

#### What is the difference between a mutex and a semaphore? Which one would you use to protect access to an increment operation?

[A mutex](http://www.jacopretorius.net/2010/12/google-interview-questions-and-answers.html) is used when only one thread or process is allowed to access a resource and a semaphore is used when only a certain set limit of threads or processes can access the shared resource. 

It looks like a mutex is a binary semaphore. __But the expected answer is mutex__.

__[A big differences](http://www.chiefdelphi.com/forums/showthread.php?p=983786) is that mutexes have the concept of "ownership"__. Only the thread that owns the mutex (i.e. was the thread that originally claimed the mutex) can give it up. If another thread tries to free the mutex, this will cause an error. With semaphores, basically any thread is allowed to manipulate them. 

#### What is multithreaded programming? What is a deadlock? 

[Multithreading](http://www.programsquare.com/2011/05/what-is-multithreaded-programming-what.html) as a widespread programming and execution model allows multiple threads to exist within the context of a single process. 

These threads share the process' resources but are able to execute independently.

__Deadlock refers to a specific condition when two or more processes are each waiting for the other to release a resource__, or more than two processes are waiting for resources in a circular chain 

In an operating system, a [deadlock is a situation](http://en.wikipedia.org/wiki/Deadlock) which occurs when a process or thread enters a waiting state because a resource requested is being held by another waiting process, which in turn is waiting for another resource. 
