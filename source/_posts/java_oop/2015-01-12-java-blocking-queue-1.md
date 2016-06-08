---
layout: post
title: "[Java OOP] Java BlockingQueue (1) "
comments: true
category: Java OOP
tags: [ src ]
---

### Overview

__[A blocking queue](http://tutorials.jenkov.com/java-concurrency/blocking-queues.html)__ is a queue that blocks when you try to __dequeue from a empty queue__, or if you try to __enqueue items into a full queue__. 

{% img middle /assets/images/blocking-queue.png %}

#### Details 

1. BlockingQueue __doesn’t accept null values__. Otherwise throw NullPointerException.

1. BlockingQueue implementations are __thread-safe__. All queuing methods are atomic in nature and use internal locks or other forms of concurrency control.

1. BlockingQueue interface is part of java collections framework and it’s primarily used for implementing __producer consumer problem__. 

Two important methods: 

1. put(E e): This method is used to insert elements to the queue, if the queue is full it waits for the space to be available.

1. E take(): This method retrieves and remove the element from the head of the queue, if queue is empty it waits for the element to be available.

#### Usage

[BlockingQueue is typically used](http://tutorials.jenkov.com/java-util-concurrent/blockingqueue.html) to have one thread produce objects, with another thread consumes (producer consumer problem). Refer to __[Design] Producer Consumer Problem__. 

### Example 1

This example shows __how changing the speed of consuming and producing__ results in different sequence of outputs, using a BlockingQueue. The size of the BlockingQueue is initialized at 5. 

    public class Main {

        // original post from:
        // http://www.journaldev.com/1034/java-blockingqueue-example-implementing-producer-consumer-problem

        private static final Setting testFullQueue = new Setting(3, 10, 0);
        private static final Setting testEmptyQueue = new Setting(10, 3, 100);

        public static void main(String[] args) {

            // Creating BlockingQueue of size 5
            BlockingQueue<Message> queue = new ArrayBlockingQueue<>(5);

            Setting variableSetting = testFullQueue;
            Producer producer = new Producer(queue, variableSetting.produceSpeed);
            Consumer consumer = new Consumer(queue, variableSetting.consumeSpeed,
                    variableSetting.consumerDelay);

            // starting producer to produce messages in queue
            new Thread(producer).start();

            // starting consumer to consume messages from queue
            new Thread(consumer).start();

            System.out.println("Producer and Consumer has been started");
        }

        static class Setting {
            int produceSpeed;
            int consumeSpeed;
            int consumerDelay;

            public Setting(int a, int b, int c) {
                this.produceSpeed = a;
                this.consumeSpeed = b;
                this.consumerDelay = c;
            }
        }
    }

Producer

    public class Producer implements Runnable {

        private BlockingQueue<Message> queue;
        int produceSpeed;

        public Producer(BlockingQueue<Message> q, int a) {
            this.queue = q;
            this.produceSpeed = a;
        }

        @Override
        public void run() {
            // produce messages
            for (int i = 0; i < 13; i++) {
                Message msg = new Message("" + i);
                try {
                    Thread.sleep(produceSpeed);
                    queue.put(msg);
                    System.out.println("Produced " + msg.getMsg() + "           ("
                            + queue.size() + " items)");
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            // adding exit message
            Message msg = new Message("exit");
            try {
                queue.put(msg);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

    }

Consumer

    public class Consumer implements Runnable {

        private BlockingQueue<Message> queue;
        int consumeSpeed;
        int consumerDelay;

        public Consumer(BlockingQueue<Message> q, int a, int b) {
            this.queue = q;
            this.consumeSpeed = a;
            this.consumerDelay = b;
        }

        @Override
        public void run() {
            try {
                // initial delay: used to wait for producer to
                // fill up the queue
                Thread.sleep(consumerDelay);
                Message msg;
                // consuming messages until exit message is received
                while ((msg = queue.take()).getMsg() != "exit") {
				System.out.println("         " + msg.getMsg() + " Consumed"+ "  ("
						+ queue.size() + " items)");
                    Thread.sleep(consumeSpeed);
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("Consumer finished working. Exit. ");
        }
    }

Message Class

    public class Message {
        private String msg;

        public Message(String str){
            this.msg=str;
        }

        public String getMsg() {
            return msg;
        }
    }

Output (testFullQueue): 

    Producer and Consumer has been started
    Produced 0           (0 items)
             0 Consumed  (0 items)
    Produced 1           (1 items)
    Produced 2           (2 items)
             1 Consumed  (1 items)
    Produced 3           (2 items)
    Produced 4           (3 items)
    Produced 5           (4 items)
             2 Consumed  (3 items)
    Produced 6           (4 items)
    Produced 7           (5 items)
             3 Consumed  (5 items)
    Produced 8           (5 items)
             4 Consumed  (4 items)
    Produced 9           (5 items)
             5 Consumed  (4 items)
    Produced 10           (5 items)
             6 Consumed  (4 items)
    Produced 11           (5 items)
             7 Consumed  (4 items)
    Produced 12           (5 items)
             8 Consumed  (4 items)
             9 Consumed  (4 items)
             10 Consumed  (3 items)
             11 Consumed  (2 items)
             12 Consumed  (1 items)
    Consumer finished working. Exit. 

Output (testEmptyQueue):

    Producer and Consumer has been started
    Produced 0           (1 items)
    Produced 1           (2 items)
    Produced 2           (3 items)
    Produced 3           (4 items)
    Produced 4           (5 items)
    Produced 5           (5 items)
             0 Consumed  (5 items)
             1 Consumed  (4 items)
             2 Consumed  (3 items)
    Produced 6           (4 items)
             3 Consumed  (3 items)
             4 Consumed  (2 items)
    Produced 7           (3 items)
             5 Consumed  (2 items)
             6 Consumed  (1 items)
             7 Consumed  (0 items)
    Produced 8           (1 items)
             8 Consumed  (0 items)
    Produced 9           (1 items)
             9 Consumed  (0 items)
    Produced 10           (1 items)
             10 Consumed  (0 items)
    Produced 11           (0 items)
             11 Consumed  (0 items)
    Produced 12           (1 items)
             12 Consumed  (0 items)
    Consumer finished working. Exit. 
