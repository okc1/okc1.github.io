---
layout: post
title: "[Design] Difference between HTTP and HTTPS "
comments: true
category: Design

---

[ref](http://stackoverflow.com/a/8375247)

#### 1: What are benefits of using HTTPS over HTTP?

HTTPS means that you __tunnel the HTTP protocol over TLS/SSL__ which encrypts the HTTP payload. 

So the benefit is that HTTP requests and responses are transmitted securely over the wire, e.g. your Internet Service Provider does not know what you're doing.

[When Google switched Gmail to use HTTPS](http://stackoverflow.com/a/548042), no additional resources were required; no network hardware, no new hosts. It only increased CPU load by about 1%.

#### 2: How to use HTTPS?

Enable it at your endpoint, in general __a web server in front of your application server__. Most web servers (e.g. IIS, Apache) support this by configuration. Depending on your confidentiality requirements this may not be enough.

#### 3: Can we use HTTPS for only login purpose and then onwords HTTP?

Technically this is possible, but it introduces some security risks. Example: After a secured login you transmit session IDs identifying the user. If you transmit those session IDs unsecurely (no SSL), session hijacking becomes a risk ('man-in-the-middle')

#### 4: What settings needs to be done for making website HTTPS?

See #2. In public internet scenarios you should request (buy) a certificate from a certain Certificate Authority (CA), so that end user clients can verify whether they should trust your certificate.

#### 5: Is there any threat present in HTTPS?

In the protocol itself there is a slight risk of __man-in-the-middle attacks__. E.g. a proxy between the client and server could pretend to be the server itself (this requires a successful attack to network infrastructure, e.g. DNS). There are several other 'more obscure' risks that do not relate to the protocol itself, e.g.:

1. usage of an outdated encryption key length (e.g. 256 bit)
1. loss of private keys or unappropriate key management procedures (e.g. send via unencrypted email)
1. certificate authority failure

#### 6: Is processing time required for HTTPS is greater than HTTP?

Yes, key negotiation (handshaking) __requires a lot CPU capacity__.

{% img middle /assets/images/http-vs-https.png %}

### Port Number

HTTP uses __port 80 or 8080__, while HTTPS uses __TCP port 443__. 

[The reason](http://www.coderanch.com/t/168608/java-Web-Component-SCWCD/certification/Diff) that some applications use 8080 (7080, 9080) instead of 80 is that on UNIX, __port numbers below 1024__ are reserved for __super-user__ processes. 

That's why for OS compatibility reasons, some servers use other ports (greater than 1024). But they still have "80" inside the numner, eg. 7080, 8080, 9080. 
