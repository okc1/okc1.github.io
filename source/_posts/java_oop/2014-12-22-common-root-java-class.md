---
layout: post
title: "[Java OOP] Common Root of Java Classes "
comments: true
category: Java OOP

---

### Common Root Class

__java.lang.Object__, [link](http://docs.oracle.com/javase/7/docs/api/java/lang/Object.html)

All Java classes are derived from this [common root class](http://www.ntu.edu.sg/home/ehchua/programming/java/J3b_OOPInheritancePolymorphism.html), that defines common behaviors.

Common behaviors include multi-threading and garbage collector etc.

#### Some methods

[ref](http://docs.oracle.com/javase/tutorial/java/IandI/objectclass.html)

protected Object clone() throws CloneNotSupportedException
> Creates and returns a copy of this object.

public boolean equals(Object obj)
> Indicates whether some other object is "equal to" this one.

protected void finalize() throws Throwable
> Called by the garbage collector on an object when garbage collection determines that there are no more references to the object

public final Class getClass()
> Returns the runtime class of an object.

public int hashCode()
> Returns a hash code value for the object.

public String toString()
> Returns a string representation of the object.

### Sync-related methods

The notify, notifyAll, and wait methods of Object all play a part in synchronizing the activities of independently running threads in a program. 

    public final void notify()
    public final void notifyAll()
    public final void wait()
    public final void wait(long timeout)
    public final void wait(long timeout, int nanos)
