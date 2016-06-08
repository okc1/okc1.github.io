---
layout: post
title: "[CC150v4] 3.4 Towers of Hanoi "
comments: true
category: CC150v4

---

### Question

> In the classic problem of the Towers of Hanoi, you have 3 rods and N disks of di!erent sizes which can slide onto any tower. The puzzle starts with disks sorted in ascending order of size from top to bottom (e.g., each disk sits on top of an even larger one). You have the following constraints:

1. Only one disk can be moved at a time.
1. A disk is slid o! the top of one rod onto the next rod.
1. A disk can only be placed on top of a larger disk.

> Write a program to move the disks from the "rst rod to the last using Stacks. 

### Solution

This is a __classic recursive question__. The solution code is supposed to be very concise. 

### Code

__written by me__, slightly different from the answer in the book, but good. 

Main class:

    public class HanoiMyAnswer {

        private static Rod r0, r1, r2;
        private static final int NUM_DISKS = 5;

        public static void main(String[] args) {
            // Hanoi Tower always have 3 rods
            r0 = new Rod(0);
            r1 = new Rod(1);
            r2 = new Rod(2);

            // Put some disks on the 1st rod, leaving 2nd and 3rd rod empty
            r0.setDisks(NUM_DISKS);

            // start main algorithm
            System.out.println("My answer: ");
            moveDisks(NUM_DISKS, r0, r2, r1);
        }

        private static void moveDisks(int number, Rod from, Rod to, Rod buffer) {
            if (number == 1) {
                int topValue = from.disks.pop();
                to.disks.push(topValue);
                displayMessage(topValue, from.name, to.name);
            } else {
                moveDisks(number - 1, from, buffer, to);
                int bottomValue = from.disks.pop();
                to.disks.push(bottomValue);
                displayMessage(bottomValue, from.name, to.name);
                moveDisks(number - 1, buffer, to, from);
            }
        }

        private static void displayMessage(int disk, int from, int to) {
            System.out.println("Disk[" + disk + "]: Rod" + from + "-->" + to);
        }
    }

Rod.java

    class Rod {

        int name;
        Stack<Integer> disks = new Stack<Integer>();

        public Rod(int rodIndex) {
            this.name = rodIndex;
        }

        public void setDisks(int n) {
            // this method will insert n disks on this Rod
            // the bottom disk is indexed as (n-1) and top one is 0
            disks.clear();
            for (int i = n - 1; i >= 0; i--) {
                disks.push(i);
            }
        }
    }
