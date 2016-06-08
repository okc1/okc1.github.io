---
layout: post
title: "[CC150v4] 14.6 Java HashMap Counter "
comments: true
categories:
- CC150v4
- Java OOP
tags: [ src ]
---

### Question

> Suppose you are using a map in your program, how would you count the number of times the program calls the put() and get() functions? 

### Solution

__Write a wrapper class upon the HashMap Class__, and override the ger() and put() methods. 

However, what if we have multiple instance of hashmap? __Solution is to use a static variable to count__. Some answers are found [here](http://stackoverflow.com/a/20027116). 

Good question this is! 

### Code 

	public static class MyHashMap<K, V> extends HashMap<K, V> {

		private static final long serialVersionUID = 1L;
		private static int count = 0;

		public V put(K key, V value) {
			count++;
			return super.put(key, value);
		}

		public V get(Object key) {
			count++;
			return super.get(key);
		}

		public static int getCount() {
			return count;
		}
	}
