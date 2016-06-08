---
layout: post
title: "[CC150v4] 14.5 Java Reflection "
comments: true
categories:
- CC150v4
- Java OOP
tags: [ src ]
---

### Question

> Explain what object reflection is in Java and why it is useful. 

### Solution

__[Java Reflection](http://tutorials.jenkov.com/java-reflection/index.html) makes it possible to inspect classes, interfaces, fields and methods at runtime__, without knowing the names of the classes, methods etc. at compile time. It is also possible to instantiate new objects, invoke methods and get/set field values using reflection.

For example, say you have an object of [an unknown type in Java](http://stackoverflow.com/a/37632), and __you would like to call a 'doSomething' method on it if one exists__. Java's static typing system isn't really designed to support this unless the object conforms to a known interface, __but using reflection__, your code can look at the object and find out if it has a method called 'doSomething' and then call it if you want to. Like this:

	Method method = foo.getClass().getMethod("doSomething", null);
	method.invoke(foo, null);

#### Usage in Junit

One very common use case in Java is the usage with annotations. JUnit 4, for example, will use reflection to __look through your classes for methods tagged with the @Test annotation__, and will then call them when running the unit test. 

### Code

The following example code is covered in [this post](http://tutorials.jenkov.com/java-reflection/index.html): 

	public class JavaReflection {

		public static void main(String[] args) {
			Method[] methods;

			methods = ListNode.class.getMethods();

			for (Method method : methods) {
				System.out.println(formatMethodName(method.getName() + "()")
						+ method.getDeclaringClass());
			}
		}

		private static String formatMethodName(String methodName) {
			for (int i = methodName.length(); i < 30; i++) {
				methodName += ".";
			}
			return methodName;
		}
	}
