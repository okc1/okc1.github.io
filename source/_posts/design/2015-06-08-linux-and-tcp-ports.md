---
layout: post
title: "[Design] Linux and TCP ports "
comments: true
category: Design

---

# Overview 

[a port](http://en.wikipedia.org/wiki/Port_%28computer_networking%29) is __a software construct serving as a communications endpoint__ in a computer's host operating system.

purpose of ports is to uniquely identify different applications or processes running on a single computer and thereby __enable them to share a single physical connection to a packet-switched network__ like the Internet.

The protocols that __primarily use ports__ are the Transport Layer protocols, such as TCP and UDP. 

__Port info can be viewed on Linux /etc/services files__.

## there're only 65536 ports

In TCP/IP stack, port number field is just 16bit size unsigned integer. Port number thus ranging from 0 to 65535.

## well-known ports 

__Well-known ports__ (or Privileged Ports) are those from 0 through 1023. 

+ 20 & 21: File Transfer Protocol (FTP)
+ 22: Secure Shell (SSH)
+ 23: Telnet remote login service
+ 25: Simple Mail Transfer Protocol (SMTP)
+ 53: Domain Name System (DNS) service
+ 80: Hypertext Transfer Protocol (HTTP) used in the World Wide Web
+ 110: Post Office Protocol (POP3)
+ 119: Network News Transfer Protocol (NNTP)
+ 143: Internet Message Access Protocol (IMAP)
+ 161: Simple Network Management Protocol (SNMP)
+ 194: Internet Relay Chat (IRC)
+ 443: HTTP Secure (HTTPS)
+ 465: SMTP Secure (SMTPS)

## Socket

[Socket is combination of](http://www.linuxnix.com/2011/05/important-port-numbers-linux-system-administrator.html) software Port and IP address.

## Protocol number

In an IP header, [the Protocol field identifies the service](https://technet.microsoft.com/en-us/library/cc959827.aspx) in the next higher level in the protocol stack to which data is passed. __Do not confuse this with port number, which is used for communication by TCP/UDP__. 

<table>
<tbody><tr><th>
<p>
Service</p>
</th><th>
<p>
Protocol Number</p>
</th></tr>
<tr><td>
<p>
Internet Control Message Protocol (ICMP)</p>
</td><td>
<p>
1</p>
</td></tr>
<tr><td>
<p>
Transmission Control Protocol (TCP)</p>
</td><td>
<p>
6</p>
</td></tr>
<tr><td>
<p>
User Datagram Protocol (UDP)</p>
</td><td>
<p>
17</p>
</td></tr>
<tr><td>
<p>
General Routing Encapsulation (PPTP data over GRE)</p>
</td><td>
<p>
47</p>
</td></tr>
<tr><td>
<p>
Authentication Header (AH) IPSec</p>
</td><td>
<p>
51</p>
</td></tr>
<tr><td>
<p>
Encapsulation Security Payload (ESP) IPSec</p>
</td><td>
<p>
50</p>
</td></tr>
<tr><td>
<p>
Exterior Gateway Protocol (EGP)</p>
</td><td>
<p>
8</p>
</td></tr>
<tr><td>
<p>
Gateway-Gateway Protocol (GGP)</p>
</td><td>
<p>
3</p>
</td></tr>
<tr><td>
<p>
Host Monitoring Protocol (HMP)</p>
</td><td>
<p>
20</p>
</td></tr>
<tr><td>
<p>
Internet Group Management Protocol (IGMP)</p>
</td><td>
<p>
88</p>
</td></tr>
<tr><td>
<p>
MIT Remote Virtual Disk (RVD)</p>
</td><td>
<p>
66</p>
</td></tr>
<tr><td>
<p>
OSPF Open Shortest Path First</p>
</td><td>
<p>
89</p>
</td></tr>
<tr><td>
<p>
PARC Universal Packet Protocol (PUP)</p>
</td><td>
<p>
12</p>
</td></tr>
<tr><td>
<p>
Reliable Datagram Protocol (RDP)</p>
</td><td>
<p>
27</p>
</td></tr>
<tr><td>
<p>
Reservation Protocol (RSVP) QoS</p>
</td><td>
<p>
46</p>
</td></tr>
</tbody></table>

> [When the IP packet contain TCP data](https://learningnetwork.cisco.com/thread/61029) the protocol number field will have the value 6 in it, so the payload will be sent to the TCP stack, TCP would then use the port numbers to send the data to the correct application. The same is for UDP with protocol number 17.
 
> Another way to look at the IP protocol number field is, if we didn't have this field in the IP packet header, IP would only be capable of carrying one type of data, while adding this field allowed the IP to carry multiple types of data differentiated by the protocol number, the same goes for TCP/UDP using TCP/UDP ports to serve multiple applications and Ethernet using the Ethertype, and so on.

## can multiple app bind to (or listen to) the same port?

Can't. [Because You can only have one application](http://stackoverflow.com/questions/1694144/can-two-applications-listen-to-the-same-port) listening on a single port at one time. 

> the app opens a port, gets a handle to it, and the OS notifies it (via that handle) when a client connection (or a packet in UDP case) arrives.
>
> If the OS allowed two apps to open the same port, how would it know which one to notify?


