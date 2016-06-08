---
layout: post
title: "[Java OOP] Interface extend another Interface "
comments: true
category: Java OOP

---

### Can an interface extend another interface in Java?

Yes. Just remember that you should implement the methods in [both interfaces](http://www.programmerinterview.com/index.php/java-questions/java-can-an-interface-extend-another-interface/). 

Example in Java source code [link1](http://docs.oracle.com/javase/7/docs/api/java/util/List.html), [link2](http://docs.oracle.com/javase/7/docs/api/java/util/Collection.html): 

    public interface List<E> extends Collection<E> {
    
    }

    public interface Collection<E> extends Iterable<E> {
    
    }

In conclusion, [ref](http://stackoverflow.com/questions/19546357/can-an-interface-extend-multiple-interfaces-in-java)

An interface can extend multiple interfaces.

A class can implement multiple interfaces.

However, a class can only extend a single class.

#### a special case

    interface A
    {
        void test();
    }

    interface B 
    {
        void test();
    }

    class C implements A, B
    {
        @Override
        public void test() {

        }
    }

Well, a single implementation works for the both methods. This implementation works no problem. 
