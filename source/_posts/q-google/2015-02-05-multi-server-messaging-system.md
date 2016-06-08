---
layout: post
title: "[Google] Multi-server Messaging System "
comments: true
category: q-google

---

### Question

[link](http://www.mitbbs.com/article_t/JobHunting/32547841.html)

> Multiple threads can publish and receive each other's message: 

1. whenever a thread publishes a message, all the other threads can receive and print out that message; 

1. if multiple message get published, the messages should be queued or whatever recorded and other threads can print out the message one by one; 

1. no published message should be missed by any other threads. 

### Solution

Suggested by [level 13](http://www.mitbbs.com/article_t/JobHunting/32547841.html):

> 给每个thread分一个blocking queue就完了。这题延伸开来是个很好的设计题, pubsub, messaging framework etc.

Using a blocking queue to store messages for each server. It's pretty much like consumer-producer. But here, the server takes on both roles. Read my code below, or __[Java OOP] PubSub (Publish–subscribe) pattern__ to learn about __PubSub__. 

### Code

Below is my code, it may not be the correct solution. If you would like to discuss, please leave me a comment! 

    public class MessagingServer implements Runnable {

        String serverId;
        List<MessagingServer> servers;
        BlockingQueue<String> messages;
        boolean isFinished;

        public MessagingServer(String id, List<MessagingServer> list, int qSize) {
            this.serverId = id;
            this.servers = list;
            messages = new ArrayBlockingQueue<String>(qSize);
            isFinished = false;
        }

        public void run() {
            // this would be the consumer
            // everything that is added to BlockingQueue<String> messages is printed
            while (!isFinished) {
                String msg;
                try {
                    msg = messages.take();
                    System.out.println(serverId + " says: " + msg);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }

        public void sendMessage(String msg) {
            // this is the producer

            // insert this msg in the blockingQ of all other servers
            for (MessagingServer server : servers) {
                server.messages.add(msg + " (received from " + this.serverId + ")");
            }
        }

        public void terminate() {
            this.isFinished = true;
        }
    }
