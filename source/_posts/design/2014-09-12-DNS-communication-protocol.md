---
layout: post
title: "[Design] DNS Communication Protocol "
comments: true
category: Design

---

### Question 

> What protocol is used for communicating with a DNS? 

### Answer

[Domain Name System](http://en.wikipedia.org/wiki/Domain_Name_System) (DNS) is a hierarchical distributed naming system for computers, services, or any resource connected to the Internet or a private network. It associates various information with domain names assigned to each of the participating entities. Most prominently, it translates easily memorized domain names to the numerical IP addresses needed for the purpose of locating computer services and devices worldwide. The Domain Name System is an essential component of the functionality of the Internet. 

[DNS primarily uses](http://en.wikipedia.org/wiki/Domain_Name_System#Protocol_transport) __User Datagram Protocol (UDP)__ on port number 53 to serve requests. 

DNS queries consist of a single UDP request from the client followed by a single UDP reply from the server. 
