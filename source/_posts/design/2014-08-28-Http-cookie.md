---
layout: post
title: "[Design] HTTP cookie"
comments: true
category: Design

---

### First Word

A cookie is __a small text file__ that is stored by a browser on the user’s machine. Cookies are plain text; they contain no executable code. 

Every time the user loads the website, the __browser sends the cookie back to the server__ to notify the website of the user's previous activity. 

1. Stateful information

	Such as shopping cart

1. browsing activity

	Such as log in, which button is clicked, and which page is visited

### Security

A secure cookie will only be sent to the server when a request is made using SSL and the HTTPS protocol. However, the entire mechanism is inherently insecure. 

The cookie just contains data and __isn’t harmful__ in and of itself. However, tracking cookies and especially third-party tracking cookies are commonly used as ways to compile long-term records of individuals' browsing history, which is a potential privacy concern. 

### Types of HTTP Cookie

Common cookie types: 

#### Session cookie

It's __while browsing__. (Normally) deleted by browser when the user closes the browser.
	
#### Persistent cookie

Max-age 1 year. The value set in that cookie would be sent back to the server every time the user visited the server. Also called __tracking cookies__

#### Secure cookie

The secure attribute is enabled, and is only used via HTTPS. 

#### Third-party cookie

__First-party cookies__ are cookies that belong to the same domain that is shown in the browser's address bar. __Third-party cookies__ are cookies that belong to domains different from the one shown in the address bar. 

It opens up the potential for __tracking the user's browsing history__. An example of 3rd-party: 

> As an example, suppose a user visits www.example1.com. This web site contains an advert from ad.foxytracking.com, which, when downloaded, sets a cookie belonging to the advert's domain (ad.foxytracking.com). Then, the user visits another website, www.example2.com, which also contains an advert from ad.foxytracking.com, and which also sets a cookie belonging to that domain (ad.foxytracking.com). Eventually, both of these cookies will be sent to the advertiser when loading their ads or visiting their website. The advertiser can then use these cookies to build up a browsing history of the user across all the websites that have ads from this advertiser.

#### One more thing

Nowadays ther'e a new kind of __HttpOnly cookie__ (used only when transmitting HTTP (or HTTPS) requests, thus restricting access from other, non-HTTP APIs such as JavaScript). 

[source1](http://www.nczonline.net/blog/2009/05/05/http-cookies-explained/)

[source2](http://en.wikipedia.org/wiki/HTTP_cookie)
