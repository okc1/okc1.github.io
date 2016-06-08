---
layout: post
title: "[Java OOP] Factory Pattern "
comments: true
category: Java OOP

---

### Factory Method Pattern

__Factory Method__ design pattern is one of the __2 most frequent topics__ for OOD. 

__[Factory method pattern](http://en.wikipedia.org/wiki/Factory_method_pattern)__ is a creational pattern which uses __factory methods__ to deal with the problem of creating objects without specifying the exact class of object that will be created. 

This is done by creating objects via factory method, either:

1. specified in an interface/abstract class and implemente (differently)
1. implemented in a base class, and be overridden in derived classes

#### in Java

A normal [Maze Game](http://en.wikipedia.org/wiki/Factory_method_pattern#Java):

    public class MazeGame {
        public MazeGame() {
            Room room1 = makeRoom();
            Room room2 = makeRoom();
            room1.connect(room2);
            this.addRoom(room1);
            this.addRoom(room2);
        }

        protected Room makeRoom() {
            return new OrdinaryRoom();
        }
    }

A magic game:

    public class MagicMazeGame extends MazeGame {
        @Override
        protected Room makeRoom() {
            return new MagicRoom();
        }
    }
