---
layout: post
title: "[Java OOP] Singleton, 3 implementations "
comments: true
category: Java OOP

---

### Implement Singlton

[3 ways](http://javarevisited.blogspot.sg/2012/07/why-enum-singleton-are-better-in-java.html) of writing Singleton. 

#### using Enum

This is only available since Java 6.

	public enum Singleton_Enum {
		INSTANCE;
	}

#### using double checked locking

This is __lazy loaded thread-safe__ Singleton, which is popular during Java 5 (with the use of Volatile variable). 

	public class Singleton_DoubleCheckedLocking implements Cloneable {
		private static volatile Singleton_DoubleCheckedLocking INSTANCE;

		private Singleton_DoubleCheckedLocking() {
		}

		public static Singleton_DoubleCheckedLocking getInstance() {
			if (INSTANCE == null) {
				synchronized (Singleton_DoubleCheckedLocking.class) {
					// double checking Singleton instance
					if (INSTANCE == null) {
						INSTANCE = new Singleton_DoubleCheckedLocking();
					}
				}
			}
			return INSTANCE;
		}
	}

#### using static factory method

Singleton instance is [static and final variable](http://javarevisited.blogspot.sg/2012/07/why-enum-singleton-are-better-in-java.html) it initialized when class is first loaded into memeory so creation of instance is inherently __thread-safe__. 

	public class Singleton_StaticFactory {
		// initailzed during class loading
		private static final Singleton_StaticFactory INSTANCE = new Singleton_StaticFactory();

		// to prevent creating another instance of Singleton
		private Singleton_StaticFactory() {
		}

		public static Singleton_StaticFactory getSingleton() {
			return INSTANCE;
		}
	}

### About thread-safety

[Prior to Java 5](http://javarevisited.blogspot.sg/2012/12/how-to-create-thread-safe-singleton-in-java-example.html) __double checked locking__ mechanism is used to create thread-safe singleton in Java, which breaks if one Thread doesn't see instance created by other thread at same time and eventually you will end up with more than one instance of Singleton class. 

From Java 5 onwards __volatile variable__ guarantee can be used to write thread safe singleton by using double checked locking pattern. 

I personally don't prefer that way as there are many other simpler alternatives like: 

1. using static field
1. using Enum 

### Q & A

Question: How do you prevent for creating another instance of Singleton using clone() method?

Answer: Preferred way is not to implement Clonnable interface. And if you do, just throw Exception from clone() method as "Can not create clone of Singleton class". 
