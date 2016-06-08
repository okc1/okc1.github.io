---
layout: post
title: "[Design] HTTP Headers"
comments: true
category: Design

---

## Overview

__HTTP is an Application Layer protocol__ which stands for "Hypertext Transfer Protocol". The entire World Wide Web uses it. 

There're __[a series of sessions](http://www.differencebetween.net/technology/internet/difference-between-tcp-and-http/)__ in HTTP where client sends a request and server sends a reply message back to client including the request, an error message, or another piece of information. 

[HTTP headers](http://code.tutsplus.com/tutorials/http-headers-for-dummies--net-8039) are the core part of these HTTP requests and responses, and they carry information about the client browser, the requested page, the server and more. 

### Example HTTP request

    GET /tutorials/other/top-20-mysql-best-practices/ HTTP/1.1
    Host: net.tutsplus.com
    User-Agent: Mozilla/5.0 (Windows; U; Windows NT 6.1; en-US; rv:1.9.1.5) Gecko/20091102 Firefox/3.5.5 (.NET CLR 3.5.30729)
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
    Accept-Language: en-us,en;q=0.5
    Accept-Encoding: gzip,deflate
    Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.7
    Keep-Alive: 300
    Connection: keep-alive
    Cookie: PHPSESSID=r2t5uvjq435r4q7ib3vtdjq120
    Pragma: no-cache
    Cache-Control: no-cache

### Example HTTP response

    HTTP/1.x 200 OK
    Transfer-Encoding: chunked
    Date: Sat, 28 Nov 2009 04:36:25 GMT
    Server: LiteSpeed
    Connection: close
    X-Powered-By: W3 Total Cache/0.8
    Pragma: public
    Expires: Sat, 28 Nov 2009 05:36:25 GMT
    Etag: "pub1259380237;gz"
    Cache-Control: max-age=3600, public
    Content-Type: text/html; charset=UTF-8
    Last-Modified: Sat, 28 Nov 2009 03:50:37 GMT
    X-Pingback: http://net.tutsplus.com/xmlrpc.php
    Content-Encoding: gzip
    Vary: Accept-Encoding, Cookie, User-Agent

    <!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
    <title>Top 20+ MySQL Best Practices - Nettuts+</title>
    <!-- ... rest of the html ... -->

These HTTP requests are also sent and received for other things, such as images, CSS files, JavaScript files etc. That is why browser may send 40 or more HTTP requests for 1 article page. 

### Request Methods

The three most commonly used request methods are: GET, POST and HEAD. 

#### GET: Retrieve a Document

Get an article site: 

    GET /tutorials/other/top-20-mysql-best-practices/ HTTP/1.1

Submit a form information: 

    GET /foo.php?first_name=John&last_name=Doe&action=Submit HTTP/1.1

Each input is added in the __query string__. 

#### POST: Send Data to the Server 

Even though you can send data to the server using GET and the query string, __in many cases POST will be preferable__. Sending large amounts of data using GET is not practical and has limitations.

    POST /foo.php HTTP/1.1
    Host: localhost
    User-Agent: Mozilla/5.0 (Windows; U; Windows NT 6.1; en-US; rv:1.9.1.5) Gecko/20091102 Firefox/3.5.5 (.NET CLR 3.5.30729)
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
    Accept-Language: en-us,en;q=0.5
    Accept-Encoding: gzip,deflate
    Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.7
    Keep-Alive: 300
    Connection: keep-alive
    Referer: http://localhost/test.php
    Content-Type: application/x-www-form-urlencoded
    Content-Length: 43

    first_name=John&last_name=Doe&action=Submit

The header contains no query string no more. The last line (data) is the query string. 

#### HEAD: Retrieve Header Information 

HEAD is identical to GET, except the server does not return the content in the HTTP response. It's faster than GET. 

