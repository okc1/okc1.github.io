---
layout: post
title: "[Design] Speed Up Webpage for Slow Connection (3) "
comments: true
category: Design

---

### Website KPI

There are [3 interesting phases](https://community.compuwareapm.com/community/display/PUB/Best+Practices+on+Web+Site+Performance+Optimization) of a web site from an end-user performance perspective. 

1. First Impression
1. OnLoad 
1. Fully Loaded Time.

### Loading Time

__Question: what percentage of the time a user spends waiting for your page to load is spent after the HTML comes back to their browser__? 

It is typically __[over 90%](http://www.sitepoint.com/seven-mistakes-that-make-websites-slow/)__. 

Most of the time users spend waiting on your website is spent after the HTML page has been retrieved by their browser. 

#### Fetching the HTML is just the beginning

__In a nutshell, browsers parse your page’s HTML, sequentially discovering its assets__ (such as scripts, stylesheets, and images), requesting and then either parsing and executing them or displaying them as appropriate. 

But these assets are not simply fetched all at once. Instead, the __browser opens a limited number of connections to the server(s)__ referenced by the page. There is __overhead involved in establishing TCP and HTTP connections__, and some __unavoidable latency__ in pushing the request and response bytes back and forth across the network.

So, in general, round trips between the browser and server are expensive. The structure of the HTML markup, the number and the ordering of its assets, are absolutely critical factors in its performance.
