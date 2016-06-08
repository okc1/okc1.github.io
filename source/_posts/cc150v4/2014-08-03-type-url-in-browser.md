---
layout: post
title: "[CC150v4] 17.1 Type a URL in Browser and Hit Enter "
comments: true
category: CC150v4

---

### Question 

17.1 Explain what happens, step by step, after you type a URL into a browser Use as much detail as possible. 

### Short Answer

1. Browser contacts the DNS server to find the IP address of URL
1. DNS returns back the IP address of the site
1. Browser opens TCP connection to the web server at port 80
1. The browser sends a GET request to the server, asking for the file 
1. Browser fetches the html code 
1. Browser renders the HTML in the display window
1. Browser terminates the connection when window is closed

[ref](http://superuser.com/q/157408)

### More Details

Phase 1: 

1. browser checks cache; if requested object is in cache and is fresh, skip to Phase 3 #4
1. browser asks OS for server's IP address
1. OS makes a DNS lookup and replies the IP address to the browser
1. browser opens a TCP connection to server (this step is much more complex with HTTPS)
1. browser sends the HTTP request through TCP connection

[ref](http://stackoverflow.com/a/2092602)

Phase 2: 

1. That computer receives the HTTP request from the TCP/IP connection and passes it to the web server program.
1. Web server reads the hostname and path and finds or generates the data that you've asked for.
1. Web server generates an HTTP response containing that data.
1. Web server sends that HTTP response back down the TCP/IP connection to your machine.

[ref](http://superuser.com/a/31474)

Phase 3: 

1. browser receives HTTP response and may close the TCP connection, or reuse it for another request
1. browser checks if the response is a redirect (3xx result status codes), authorization request (401), error (4xx and 5xx), etc.; these are handled differently from normal responses (2xx)
1. if cacheable, response is stored in cache
1. browser decodes response (e.g. if it's gzipped)
1. browser determines what to do with response (e.g. is it a HTML page, is it an image, is it a sound clip?)
1. browser renders response, or offers a download dialog for unrecognized types

### Miscellaneous:

Each domain name server is divided into zones A single server may only be responsible for knowing the host names and IP addresses for a small subset of a zone, but DNS servers can work together to map all domain names to their IP addresses That means if one domain name server is unable to find the IP addresses of a requested domain then it requests the information from other domain name servers

The firewall will control connections to & from your computer. For the most part it will just be controlling who can connect to your computer and on what ports. For web browsing your firewall generally won't be doing a whole lot.

Your router essentially guides your request through the network, helping the packets get from computer to computer and potentially doing some NAT (Network Address Tranlator) to translate IP addresses along the way (so your internat LAN request can be transitioned onto the wider internet and back).

### Even more

An even more detailed article can be found [here](http://www.garshol.priv.no/download/text/http-tut.html). And a __great step-by-step example using facebook.com can be found [here](http://igoro.com/archive/what-really-happens-when-you-navigate-to-a-url/).
