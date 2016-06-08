---
layout: post
title: "[Design] TCP 3-Way Handshake"
comments: true
category: Design

---

### Handshaking

__[Handshaking](http://en.wikipedia.org/wiki/Handshaking) is an automated process of negotiation__ that dynamically sets parameters of a communications channel established between two entities before normal communication over the channel begins. 

It is usually a process that takes place when a computer is about to communicate with a foreign device to establish rules for communication. 

### TCP three-way handshake

__[TCP three-way handshake](http://www.inetdaemon.com/tutorials/internet/tcp/3-way_handshake.shtml)__ is the method used by TCP set up a TCP/IP connection over an Internet Protocol based network. 

It's commonly referred to as "__SYN-SYN-ACK__". 

{% img middle /assets/images/3way-Tcp-handshake.png %}

### Process

1. Host A sends a TCP __SYN__chronize packet to Host B
1. Host B receives A's SYN
1. Host B sends a __SYN__chronize-__ACK__nowledgement 
1. Host A receives B's SYN-ACK
1. Host A sends __ACK__nowledge
1. Host B receives ACK. 
1. TCP socket connection is ESTABLISHED.

Alternatively, there's a good illustration on [wiki](http://en.wikipedia.org/wiki/Handshaking): 

> Establishing a normal TCP connection requires three separate steps:

> 1. The first host (Alice) sends the second host (Bob) a "synchronize" (SYN) message with its own sequence number x, which Bob receives.
>
> 1. Bob replies with a synchronize-acknowledgment (SYN-ACK) message with its own sequence number y and acknowledgement number x + 1, which Alice receives.
>
> 1. Alice replies with an acknowledgment message with acknowledgement number y + 1, which Bob receives and to which he doesn't need to reply.

### Two more thing

Note that __FTP, Telnet, HTTP, HTTPS, SMTP, POP3, IMAP, SSH__ and any other protocol that rides over TCP __also has a three way handshake__ performed as connection is opened.

TCP 'rides' on top of Internet Protocol (IP) in the protocol stack. IP handles __IP addressing and routing__ and gets the packets from one place to another, but TCP manages the __actual communication sockets__ between endpoints. 
