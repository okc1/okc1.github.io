---
layout: post
title: "[Design] Stack and Heap"
comments: true
category: Design

---

### Overview

Value types are created on the stack, and reference types are created on the heap. 

__Both are stored in computer RAM__. 

__Each thread gets a stack__, while there's typically only one heap for the application. 

#### Stack

[When a function](http://stackoverflow.com/a/80113) is called, a block is reserved __on the top of the stack__ for local variables and some bookkeeping data in a LIFO order. Freeing a block from the stack is nothing more than adjusting one pointer. 

#### Heap

Unlike the stack, there's no enforced pattern to the allocation and deallocation of blocks from the heap; you can allocate a block at any time and free it at any time. This makes it much more complex to keep track of which parts of the heap are allocated or free at any given time; there are many custom heap allocators available to tune heap performance for different usage patterns. 

### Q & A

#### What is their scope?

The stack is attached to a thread, so __when the thread exits__ the stack is reclaimed. 

The heap is typically allocated at application startup by the runtime, and is reclaimed __when the application (technically process) exits__. 

Thread and process - what's the difference? Read __[Design] Process VS. Thread__. 

#### What determines the size of each of them?

The size of the stack is set when a thread is created. 

The size of the heap is set on application startup, but can grow as space is needed (the allocator requests more memory from the operating system).

#### What makes one faster? 

__The stack is faster__ because the access pattern makes it trivial to allocate and deallocate memory from it, while the heap has much more complex bookkeeping involved in an allocation or free. 

Each byte in the stack tends to be reused very frequently which means it tends to be mapped to the processor's cache, making it very fast. 

Another performance hit for the heap is that the heap, being mostly a global resource, typically has to be multi-threading safe, i.e. each allocation and deallocation needs to be (typically) synchronized.

{% img middle /assets/images/stack-and-heap.png %}
