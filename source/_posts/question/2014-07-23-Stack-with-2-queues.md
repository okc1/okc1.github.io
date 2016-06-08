---
layout: post
title: "[Question] Implement Stack using Two Queues"
comments: true
category: Question
tags: [ src ]
---

### Question 

[link](http://stackoverflow.com/questions/688276/implement-stack-using-two-queues)

> Given two queues with their standard operations (enqueue, dequeue, isempty, size), implement a stack with its standard operations (pop, push, isempty, size).

### Analysis

There should be TWO versions of the solution.

1. __Version A__: The stack should be efficient when __pushing__ an item.

1. __Version B__: The stack should be efficient when __popping__ an item.

### Version A

The stack should be efficient when __pushing__ an item.

1. push:

    1. enqueue in queue1

1. pop: 

    1. while size of queue1 is bigger than 1, pipe dequeued items from queue1 into queue2
    1. dequeue and return the last item of queue1, then switch the names of queue1 and queue2

### Version B

The stack should be efficient when __popping__ an item. 

1. push:

    1. enqueue in queue2
    1. enqueue all items of queue1 in queue2, then switch the names of queue1 and queue2

1. pop:

    1. deqeue from queue1

[reference](http://stackoverflow.com/a/688299)

Learn and compare with another question __[Question] Implement Queue Using Stacks__. 

### Code

__written by me__, Version A. 

    public class StackBuiltWithTwoQueue {

        // http://stackoverflow.com/questions/688276/implement-stack-using-two-queues

        Queue<Integer> q1 = new LinkedList<Integer>();
        Queue<Integer> q2 = new LinkedList<Integer>();

        public static void main(String[] args) {
            StackBuiltWithTwoQueue stack = new StackBuiltWithTwoQueue();
            stack.push(1);
            stack.push(2);
            stack.push(3);
            System.out.println(stack.pop());
            stack.push(4);
            System.out.println(stack.pop());
            System.out.println(stack.pop());
            stack.push(5);
            stack.push(6);
            stack.push(7);
            stack.push(8);
            stack.push(9);
            System.out.println(stack.pop());
            System.out.println(stack.pop());
            System.out.println(stack.pop());
            System.out.println(stack.pop());
            System.out.println(stack.pop());
            System.out.println(stack.pop());
            System.out.println(stack.pop());
            System.out.println(stack.pop());
        }

        public void push(int val) {
            q1.offer(val);
        }

        public int pop() {
            if (q1.isEmpty()) {
                System.out.print("Stack is empty now ");
                return -1;
            }
            while (q1.size() > 1) {
                q2.offer(q1.poll());
            }
            int topVal = q1.poll();
            Queue<Integer> temp = q1;
            q1 = q2;
            q2 = temp;
            return topVal;
        }
    }
