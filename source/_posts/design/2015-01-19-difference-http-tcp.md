---
layout: post
title: "[Design] Difference between HTTP protocol and TCP protocol "
comments: true
category: Design

---

[ref](http://www.quora.com/What-is-the-difference-between-HTTP-protocol-and-TCP-protocol)

### Short Version

TCP is a __transport-layer__ protocol, and HTTP is an __application-layer__ protocol that runs over TCP. 

### The layers

At the very bottom of the network stack is the __physical layer__. This is where electrical signals or light pulses or radio waves actually transmit information from place to place. The physical layer doesn't really have protocols, but instead has standards for voltages, frequencies, and other physical properties. You can transmit information directly this way, but you need a lot of power or a dedicated line, and without higher layers you won't be able to share bandwidth.

The next layer up is the __link layer__. This layer covers communication with devices that share a physical communications medium. Here, protocols like Ethernet, 802.11a/b/g/n, and Token Ring specify how to handle multiple concurrent accesses to the physical medium and how to direct traffic to one device instead of another. In a typical home network, this is how your computer talks to your home "router."

The third layer is the __network layer__. In the majority of cases, this is dominated by Internet Protocol (IP). This is where the magic of the Internet happens, and you get to talk to a computer halfway around the world, without needing to know where it is. Routers handle directing your traffic from your local network to the network where the other computer lives, where its own link layer handles getting the packets to the right computer.

Now we are getting somewhere. We can talk to a computer somewhere around the world, but that computer is running lots of different programs. How should it know which one to deliver your message to? The __transport layer__ takes care of this, usually with __port numbers__. The two most popular transport layer protocols are TCP and UDP. TCP does a lot of interesting things to smooth over the rough spots of network-layer packet-switched communication like reordering packets, retransmitting lost packets, etc. UDP is more unreliable, but has less overhead.

So we've connected your browser to the web server software on the other end, but how does the server know what page you want? How can you post a question or an answer? These are things that __application-layer__ protocols handle. For __web traffic__, this is the HyperText Transfer Protocol (HTTP). There are thousands of application-layer protocols: SMTP, IMAP, and POP3 for email; XMPP, IRC, ICQ for chat; Telnet, SSH, RDP for remote administration; etc.

Ref: http://qr.ae/3pnJK
