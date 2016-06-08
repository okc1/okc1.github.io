---
layout: post
title: "[Design] Application Server vs. Web Server"
comments: true
category: Design

---

## Overview

A Web server __exclusively handles HTTP requests__, whereas an application server __serves business logic__ to application programs through any number of protocols (including HTTP). 

#### Example: Apache Tomcat

web server + servlet container

#### Example: Glassfish

__application server__ (that supports EJB, JSF, JSP and servlets)

### Apache Tomcat

Apache Tomcat is [a web server and](http://stackoverflow.com/a/2469984) a Web container/Servlet container/JSP container (having all these names). It is used for strictly web-based applications but does not include the entire suite of capabilities of Java EE, thus not application server. 

Note: __Tomcat is [web container](http://okckd.github.io/blog/2014/08/05/Web-server-application-server/)__ where as Apache is web server.

### Servlet

[A servlet](https://tomcat.apache.org/tomcat-5.5-doc/servletapi/javax/servlet/Servlet.html) is __a small Java program that runs within a Web server__. Servlets receive and respond to requests from Web clients, usually across HTTP. 

### Glassfish 

Tomcat is not Java EE container, but only a servlet container. [If you plan to](http://stackoverflow.com/a/23563455) use full Java EE (which includes security and many other things), you have to switch from Tomcat to some of __full Java EE application servers__. Glassfish is one of them, others are TomEE, WildFly, IBM Websphere, Oracle Weblogic etc. 

### Web application

[A Web application](http://www.service-architecture.com/articles/application-servers/j2ee_web_server_or_container.html) runs within a __Web container__ of a __Web server__. The Web container provides the runtime environment through components that provide naming context and life cycle management. A Web server __may__ work with an EJB server to provide some of those services.

Web applications are composed of web components and other data such as HTML pages. Web components can be __servlets, JSP pages__ created with the JavaServer Pages™ technology, web filters, and web event listeners. These components execute in a web server and may respond to HTTP requests from web clients. 

### Application server VS. Web server, in short

__Web server__ just serves the web pages and it cannot enforce any application logic.

__Application server__ maintains the application logic and serves the web pages in response to user request.

That means application server can do both application logic maintanence and web page serving.

__Final conclusion__: Application server also contains the web server.

> Application server = Web Server + EJB container. 

### Web server Detail

A [Web server](http://www.javaworld.com/article/2077354/learn-java/app-server-web-server-what-s-the-difference.html) __handles the HTTP protocol__. When the Web server receives an HTTP request, it responds with an HTTP response, such as sending back an HTML page. 

To process a request, a Web server may __respond with a static HTML page__, or delegate the __dynamic response__ such as CGI scripts, JSPs (JavaServer Pages), servlets, ASPs (Active Server Pages), server-side JavaScripts, or some other server-side technology. 

Web server is used only for Jsp and Servlets and static functionality. It doesn’t support EJB and JMS and JAAS.

### Application server Detail

An [Application server](http://www.javaworld.com/article/2077354/learn-java/app-server-web-server-what-s-the-difference.html) __exposes business logic to client applications__ through various protocols, possibly including HTTP. The clients can include GUIs (graphical user interface) running on a PC, a Web server, or even other application servers. 

In most cases, the server exposes this business logic through a component API, such as the EJB (Enterprise JavaBean) component model found on J2EE (Java 2 Platform, Enterprise Edition) application servers.

### Example

There's [a nice example](http://www.javaworld.com/article/2077354/learn-java/app-server-web-server-what-s-the-difference.html): online store that provides real-time pricing. 

#### Scenario 1: Web server

The Web server takes your request, then passes it to a server-side program able to handle the request. The server-side program looks up the pricing information from a database or a flat file. Once retrieved, the server-side program uses the information to formulate the HTML response, then the Web server sends it back to your Web browser.

To summarize, a Web server simply processes HTTP requests __by responding with HTML pages__.

#### Scenario 2: Web server with an application server

Scenario 2 resembles Scenario 1 in that the Web server still delegates the response generation to a script. However, you can now put the business logic for the pricing lookup onto an application server. 

With that change, instead of the script knowing how to look up the data and formulate a response, the script can simply call the application server's lookup service. The script can then use the service's result when the script generates its HTML response.

In this scenario, the application server serves the business logic for looking up a product's pricing information. That functionality doesn't say anything about display or how the client must use the information. Instead, the client and application server send data back and forth. When a client calls the application server's lookup service, the service simply looks up the information and returns it to the client.

By separating the pricing logic from the HTML response-generating code, the pricing logic becomes far more reusable between applications. A second client, such as a cash register, could also call the same service as a clerk checks out a customer. In contrast, in Scenario 1 the pricing lookup service is not reusable because the information is embedded within the HTML page. To summarize, in Scenario 2's model, the Web server handles HTTP requests by replying with an HTML page while the application server serves application logic by processing pricing and availability requests.
