---
layout: post
title: "[Design] Speed Up Webpage for Slow Connection (2) "
comments: true
category: Design

---

(... continued from last post)

#### 9. Use a Content Delivery Network (CDN)

Your site’s speed is greatly affected by where the user’s location is, relative to your web server. The farther away they are, the more distance the data being transmitted has to travel. Having your content cached __across multiple, strategically placed geographical locations__ helps take care of this problem. 

A CDN will often make your operating cost a little higher, but you definitely gain a speed bonus. Check out MaxCDN or __Amazon Simple Storage Service (Amazon S3)__.

#### 10. Optimize Web Caching

Along with using caching systems, you should create websites that utilize __web caching__ as much as possible. Web caching is when files are __cached by the web browser__ for later use. Things that browsers can cache include CSS files, JavaScript files, and images.

Aside from the basics, such as putting CSS and JavaScript code that are used in multiple pages in external files, there are many ways to make sure that you are caching your files in the most efficient way possible.

For example, you can set HTTP response headers such as Expires and Last-Modified to reduce the need of re-downloading certain files when the user comes back to your site. To learn more, read about [caching in HTTP](http://www.w3.org/Protocols/rfc2616/rfc2616-sec13.html) and [leveraging browser caching](https://developers.google.com/speed/docs/insights/LeverageBrowserCaching?csw=1#LeverageBrowserCaching).

To set up HTTP Expires headers in Apache, read this tutorial on adding future expires headers.

#### Other mentions

4. __Avoid Resizing Images in HTML__ (using HTML’s width and height attributes), for the sake of smaller file size. 

6. __Optimize Image Sizes by Using the Correct File Format__. Eg. JPG format often displays photographic images at smaller file sizes than PNG. 

7. __Optimize the Way You Write Code__. For example, instead of using (h1)(em)Your heading(em)(h1), you can easily use CSS to make your headings italics. 

    Writing code efficiently not only reduces file sizes of your HTML and CSS documents, but also makes it easier to maintain.

Ref: http://sixrevisions.com/web-development/site-speed-performance/
