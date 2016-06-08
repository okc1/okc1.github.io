---
layout: post
title: "[Java OOP] Can abstract class have constructor "
comments: true
category: Java OOP

---

# A short answer

In Java, all classes must have a constructor.

## Can abstract class have constructor

[Yes, it can](http://www.mitbbs.com/article_t/JobHunting/32257933.html). However, if we create an instance using it, it's error. 

Consider [this example](http://www.geeksforgeeks.org/abstract-classes-in-java/): 

    abstract class Base {
        Base() { System.out.println("Base Constructor Called"); }
        abstract void fun();
    }
    
    class Derived extends Base {
        Derived() { System.out.println("Derived Constructor Called"); }
        void fun() { System.out.println("Derived fun() called"); }
    }
    
    class Main {
        public static void main(String args[]) { 
           Derived d = new Derived();
        }
    }

Output:

    Base Constructor Called
    Derived Constructor Called

## More info on constructor: 

The [constructor in an abstract class](http://stackoverflow.com/a/261159): 

1. is used when you want to perform some initialization
1. you may define more than one constructor (with different arguments)
1. if you don't define a constructor, then the compiler will automatically generate one for you.
1. your subclass constructor __have to call a constructor__ from the abstract class
1. you can define all your constructors protected (cuz making them public is pointless)

For more on abstract class, read __[Java OOP] Template method pattern__.
