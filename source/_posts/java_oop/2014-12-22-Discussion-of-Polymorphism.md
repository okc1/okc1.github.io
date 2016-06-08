---
layout: post
title: "[Java OOP] Discussion of Polymorphism "
comments: true
category: Java OOP

---

# Overview

Polymorphism is to [use common interface](http://javarevisited.blogspot.sg/2011/08/what-is-polymorphism-in-java-example.html) instead of concrete implementation while coding. 

The most common use of polymorphism in OOP occurs __when a parent class reference is used to refer to a child class object__.

## Quick Summary: 

[ref](http://www.ntu.edu.sg/home/ehchua/programming/java/J3b_OOPInheritancePolymorphism.html)

1. A subclass instance can be assigned to a superclass' reference.

1. Once substituted, we can invoke methods defined in super-class; we CANNOT invoke methods from sub-class.

1. if sub-class overrides inherited methods from the super-class, the overridden versions will be invoked.

1. Reference cannot point to superclass.

## Advantages

1. Simpler programs

    eg.
    superRef[] = new Circle[2];
    superRef[0] = new Cylinder();
    superRef[1] = new Circle();
    
    > Just 1 single array to represent different objects

1. Better re-usability

## A practical example

Cylinder is a subclass of Circle. We gonna do this:

> Circle c1 = new Cylinder();

The code is below: 

    public class PolymorphismSubstitutabilityDemo {

        public static void main(String[] args) {
            Circle c1 = new Cylinder(1, "white", 10);
            System.out.println(c1.getClass());
            System.out.println(c1.getRadius());
            System.out.println(c1.getArea());
        }
    }

    class Circle {
        int radius;
        String color;

        public Circle(int a, String b) {
            this.radius = a;
            this.color = b;
        }

        public int getRadius() {
            return radius;
        }

        public double getArea() {
            return 3.14159 * Math.pow(radius, 2);
        }
    }

    class Cylinder extends Circle {
        int height;

        public Cylinder(int a, String b, int c) {
            super(a, b);
            this.height = c;
        }

        public double getArea() {
            return super.getArea() * height;
        }
    }

The output of execution: 

    class Cylinder
    1
    31.4159
