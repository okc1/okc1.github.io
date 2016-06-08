---
layout: post
title: "[CC150v5] 14.6 Implement CircularArray in Java "
comments: true
category: CC150v5
tags: [ src ]
---

### Question

> Implement a __CircularArray__ class that supports an array-like data structure which can be efficiently rotated. 

> The class should use a generic type, and should support iteration via the standard for (Object : circuLarArray) notation. 

### Solution

__First part of the question is solved by using an array and a pointer__. The solution simplifies the question by fixing the array size (not a dynamic-resizing array). 

__The difficult part is how to write iterator__.

Note that we should support __Java Generics__:

    class MyCircularArray<T>

Implement __Iterable Interface__:

    public class MyCircularArray<T> implements Iterable<T> {
    }

Override __iterator() method__:

	@Override
	public Iterator<T> iterator() {
		return new MyIterator<T>(this);
	}

Write our own __Iterator Class__:

	class MyIterator<T> implements Iterator<T> {
    }

Finish it up

    public class MyCircularArray<T> implements Iterable<T> {

        @Override
        public Iterator<T> iterator() {
            return new MyIterator<T>(this);
        }

        class MyIterator<T> implements Iterator<T> {
            @Override
            public boolean hasNext() {
            }

            @Override
            public T next() {
            }

            @Override
            public void remove() {
            }
        }
    }

It might be confusing when implementing __Iterable__ and __Iterator__ Class.

### Code

    public class MyCircularArray<T> implements Iterable<T> {

        T[] items;

        int head;
        int cur;

        public MyCircularArray(int size) {
            // this is really important (casting the type)
            items = (T[]) new Object[size];

            head = 0;
            cur = 0;
        }

        public void put(T item) {
            items[cur++] = item;
            cur = cur % items.length;
        }

        public T get(int i) {
            int newIndex = (i + head) % items.length;
            return items[newIndex];
        }

        public void rotate(int shiftRight) {
            head += shiftRight;
            head = head % items.length;
        }

        @Override
        public Iterator<T> iterator() {
            return new MyIterator<T>(this);
        }

        class MyIterator<T> implements Iterator<T> {

            T[] items;
            int head;
            int count;

            public MyIterator(MyCircularArray<T> array) {
                this.items = array.items;
                this.head = array.head;
                this.count = 0;
            }

            @Override
            public boolean hasNext() {
                return this.count != items.length;
            }

            @Override
            public T next() {
                if (hasNext()) {
                    return items[(head + count++) % items.length];
                }
                return null;
            }

            @Override
            public void remove() {
            }
        }

    }
