---
layout: post
title: "[Design] Multithreading Basics"
comments: true
category: Design

---

## Terminologies

### Atomicity, Atomic Operation

__[Atomicity](http://www.geeksforgeeks.org/g-fact-57/) is unbreakability__, or uninterrupted operation.

Atomic operation helps in understanding reentrancy, critical section, thread safety, synchronization primitives, etc. 

### Critical Section

__[Critical section](http://www.geeksforgeeks.org/g-fact-70/)__ is group of instructions/statements or region of code that __need to be executed atomically__. 

If one thread tries to change a shared data while another thread tries to read, the result is unpredictable. It is critical to understand the importance of race condition while writing kernel mode programming. 

A simple solution to critical section: 

    acquireLock();
    Process Critical Section
    releaseLock();

### Synchronization primitives

[Synchronization primitives](http://stackoverflow.com/a/8017629) are simple software mechanisms for the purposes of supporting thread or process synchronization. 

__Mutex, event, conditional variables and semaphores__ are all synchronization primitives. 

__Critical section__ is not a synchronization primitive. It's a part of an execution path that must be protected from concurrent execution in order to maintain some invariants. 

You need to use some synchronization primitives to protect critical section.

### Producer–consumer

Two processes, [producer and consumer](http://en.wikipedia.org/wiki/Producer-consumer_problem). Producer thread will collect the data and writes it to the buffer. Consumer thread will process the collected data from the buffer. 

Producer won't try to add when buffer's full and consumer won't remove when buffer's empty. 

__Solution 1: Mutex__

A mutex provides mutual exclusion, either producer or consumer can have the key (mutex) and proceed with their work. As long as the buffer is filled by producer, the consumer needs to wait, and vice versa.

__Solution 2: Semaphore__

[A semaphore](http://en.wikipedia.org/wiki/Producer-consumer_problem#Using_semaphores) is a generalized mutex. In lieu of single buffer, we can split the 4 KB buffer into four 1 KB buffers (identical resources). A semaphore can be associated with these four buffers. The consumer and producer can work on different buffers at the same time.

### Interrupt service routine

[Interrupt service routine](http://en.wikipedia.org/wiki/Interrupt_handler) (ISR), is a callback subroutine in an operating system or device driver whose execution is triggered by the reception of an interrupt. 

[One good example](http://stackoverflow.com/a/3392889) is reading from a hard drive. The drive is slow and you don't want your OS to wait for the data to come back; you want the OS to go and do other things. __So you set up the system so that when the disk has the data (ready), it raises an interrupt__. In the __ISR for the disk__, CPU will take the data and return it to the requester. 

__ISRs often need to happen quickly__ as the hardware can have a limited buffer, which will be overwritten by new data if it's now pulled off quickly enough. 

It's also important to have your ISR complete quickly as while the CPU is servicing one ISR other interrupts will be masked. 
