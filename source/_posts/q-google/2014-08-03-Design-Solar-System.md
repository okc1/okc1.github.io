---
layout: post
title: "[Google] Design Solar System (`)"
comments: true
category: q-google

---

### Question 

[link](http://www.careercup.com/question?id=14761735)

> Design a web application to represent hierarchy of solar system. 

> Give details of Persistence layer, business layer, presentation layer and Client-server protocol. 

### Solution

__First, OOD part__ is very well covered in [this site](http://www.ehow.com/how_5579338_build-own-solar-system-java.html). There're 2 abstract class: __OrbitalSystem__, where 'Star/Sun' is an instance, and __GravityObject__, where 'Planet/Earch' is an instance. Though this does not take satellite into consideration. 

__Second, the multi-layer structure__. It's cover in another post __[Multilayered architecture]({% post_url /design/2014-08-03-Multilayered-architecture %})__

__Third, the protocol__. We [use HTTP protocol](http://stackoverflow.com/a/4279218), because: 

> HTTP(S) is the best protocol to use. The overhead (i.e. headers) is pretty small, the transfer can be gzipped, the connection can be secured (via SSL). Also, ports 80 (HTTP) and 443 (HTTPS) will be open in 99% of cases. Other ports are not -- for example some carriers block all other ports unless you pay extra. 

More info on HTTP communication comes later. 

### Code

from [here](http://www.ehow.com/how_5579338_build-own-solar-system-java.html)

    public abstract class GravityObject {
        double xPosition;
        double yPosition;
        double degreeInOrbit;
        double distanceFromParent;

        GravityObject() {
        this.distance = 0;
        }

        GravityObject(double distance) {
        this.distance = distance;
        }
    }

    import java.util.ArrayList;

    public abstract class OrbitalSystem extends GravityObject {
        private ArrayList children = new ArrayList(); // Objects within the system. They will orbit the parent.

        public void add(GravityObject child) { children.add(child); }

        public void tick() {
            for (int x = 0; x < children.size(); x++) {
                GravityObject current = children.get(x);
                current.degree += 1
                current.xPosition = this.xPosition + Math.cos(degree/180 * Math.PI)* current.distance;
                current.yPosition = this.yPosition - Math.sin(degree/180 * Math.PI) * current.distance;
            }
        }
    }

    public class Star extends OrbitalSystem { 

    };

    public class Planet extends GravityObject { 

    };

    public static int main(String[] args) {
        Star s = new Star(); // Create a new star.
        s.add(new Planet(20)); // Add a planet to the star's orbital system which orbits at a distance of 20 units.
        s.add(new Planet(66)); // Add another planet to the star's orbital system which orbits at a distance of 66 units.

        while (true) {
            s.tick();
        }
    }
