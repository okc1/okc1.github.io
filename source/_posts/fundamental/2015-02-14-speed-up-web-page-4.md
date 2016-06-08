---
layout: post
title: "[Design] Speed Up Webpage for Slow Connection (4) "
comments: true
category: Design

---

### What hijacks your load time

#### 1. Too Many HTTP Requests

This is the single biggest contributor to performance problems in most web pages. 

1. Concatenate scripts and stylesheets

1. Combine images with sprites (put common images into a single large image file, then use CSS to position and selectively display the appropriate portion of the sprite image)

1. Use fewer images, more CSS. 

#### 2. Minimal Client-side Processing

1. Validation on client. (eg. form input)

1. Use web standards and MVC separation, making a maintainable, accessible, future-proof and max-performance website. 

    Think of the HTML as the model, the CSS as the view, and the JavaScript as the controller. This separation tends to make code more efficient and maintainable, and makes many optimization techniques much more practical to apply.

1. Push presentation code into the client tier (eg. Charts and graphs — push raw data to the client in JSON format, and use JavaScript and CSS to create pretty graphs.)

1. Leverage Ajax techniques (only requiring small parts of the page to change in response to user actions)

#### 3. Low Number of Parallel Requests

Fetch a script, parse and execute it, then fetch another one... this will use up all the available connections. There are things you can do to your HTML to allow virtually any browser to make many requests at once, which has a huge impact on latency.

1. Use browser-appropriate domain sharding

1. Use intelligent script loading

1. Leverage Keep-Alive (reuse the same TCP connection for multiple HTTP request/response cycles)

#### 4. Failure to leverage browser cache / local storage

1. [HTTP cache overview](http://www.mnot.net/cache_docs/)

1. Leverage local storage

#### 5. Third-party widgets

1. Avoid third-party widgets!
1. Try to use widgets that provide asynchronous implementations, so their inevitably terrible performance impacts their widget without dragging down your entire UX with it.

#### 7. Failure to Use a Global Network

Amazon S3. 

Ref: http://www.sitepoint.com/seven-mistakes-that-make-websites-slow/
