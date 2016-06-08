---
layout: post
title: "[Java OOP] Static class and Inner class "
comments: true
category: Java OOP

---

# Nested classes 

Both Static class and Inner class are called __nested class__. 

[The purpose of a nested class](http://tutorials.jenkov.com/java/nested-classes.html) is to __clearly group the nested class with its surrounding class__, signaling that these two classes are to be used together. 

Now the 2 types:

1. Static nested classes (also: Static Classes )
1. Non-static nested classes (also: Inner Class)

## Static Classes 

Declare:

    public class Outer {
        public static class Nested {

        }
    }

Instantiate (just like a normal class):

    Outer.Nested instance = new Outer.Nested();

## Inner Classes 

    public class Outer {
        public class Inner {
        
        }
    }

Instantiate (you MUST have an instance of enclosing class, and look weird the 'new' keyword looks):

    Outer outer = new Outer();
    Outer.Inner inner = outer.new Inner();

# access level

__Inner class__ can access private members in enclosing class (static or non-static).

    public class Outer {

        private String text = "I am private!";

        public class Inner {

            public void printText() {
                System.out.println(text);
            }
        }
    }

__Static class__ [cannot access non-static members](http://www.geeksforgeeks.org/static-class-in-java/). 

# top-level static class?

Java has __[no way of making a top-level class static](http://stackoverflow.com/a/7486111)__ but you can simulate a static class like this:

1. Declare your class final

1. Make the constructor private

1. Make all the members and functions of the class static

(this basically is a Singleton)
