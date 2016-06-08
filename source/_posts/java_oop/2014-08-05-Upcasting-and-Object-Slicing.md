---
layout: post
title: "[Java OOP] Upcasting, Downcasting and Object Slicing"
comments: true
category: Java OOP
tags: [ src ]
---

### Upcasting and Downcasting

Java permits an object of a __subclass type to be treated as an object of any superclass type__. This is [called upcasting](http://forum.codecall.net/topic/50451-upcasting-downcasting/). Upcasting is done automatically, while downcasting must be manually done. 

[Example](http://forum.codecall.net/topic/50451-upcasting-downcasting/):

{% img middle /assets/images/java-upcasting-downcasting.jpg %}

	Cat c1 = new Cat();
	Animal a = c1; //automatic upcasting to Animal
	Cat c2 = (Cat) a; //manual downcasting back to a Cat

Upcasting is always typesafe but can cause the so called ["slicing" problem](http://forums.codeguru.com/showthread.php?321676-What-are-upcasting-and-downcasting-dangers). 

### Object Slicing

[Object slicing](https://www.java.net/also-in-java/object-slicing-and-component-design-java) is defined as the conversion of an object into something with less information (typically a superclass)

### More detail

If you upcast an object, it will __lose all it's properties__, which were inherited. For example, if you cast a Cat to an Animal, it will lose properties inherited from Mammal and Cat. Note, that __data will not be lost, you just can't use it__, until you downcast the object to the right level. 

### Example 

	class Base {
		void doSomething() {
			System.out.println("Base");
		}
	}

	class Derived extends Base {
		void doSomething() {
			System.out.println("Derived");
		}
	}

	public class JavaUpcasting {
		public static void main(String[] args) {
			Base instance = new Derived();
			instance.doSomething();
		}
	}

This will output "Derived". 
