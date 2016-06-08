---
layout: post
title: "[Design] Speed Up Webpage for Slow Connection (1) "
comments: true
category: Design

---

[ref](www.geeksforgeeks.org/amazon-interview-set-72-campus-sde-1)

### Question

> Suppose you are handling Amazon website and you have 10 MB size home page. Optimize the homepage for a customer who has 100 kbps internet connection.

> Further he asked for the customer who has 100 mbps internet connection.

### Reading

[This](http://sixrevisions.com/web-development/site-speed-performance/) is a very nice article about website speedup. Below is the full quoted text. 

#### 1. Defer Loading Content When Possible

Ajax allows us to build web pages that can be __asynchronously updated__ at any time. This means that instead of reloading an entire page when a user performs an action, we can simply update parts of that page.

We can use an image gallery as an example. Image files are big and heavy; they can slow down page-loading speeds of web pages. Instead of loading all of the images when a user first visits the web page, we can just display thumbnails of the images and then when the user clicks on them, we can asynchronously request the full-size images from the server and update the page. This way, if a user only wants to see a few pictures, they don’t have to suffer waiting for all of the pictures to download. This development pattern is called __lazy loading__.

__Ajax/web development libraries__ like jQuery, Prototype, and MooTools can make deferred content-loading easier to implement.

#### 2. Use External JS and CSS Files

When the user first loads your web page, the browser will cache external resources like CSS and JavaScript files. Thus, instead of inline JavaScript and CSS files, it’s best to __place them in external files__.

Using inline CSS also increases the rendering time of a web page; having everything defined in your main CSS file lets the browser do less work when rendering the page, since it already knows all the style rules that it needs to apply.

__As a bonus__, using external JavaScript and CSS files makes site maintenance easier because you only need to maintain global files instead of code scattered in multiple web pages.

#### 3. Use Caching Systems

If you find that your site is connecting to your database in order to create the same content, it’s time to start using a __caching system__. By having a caching system in place, your site will only have to create the content once instead of creating the content every time the page is visited by your users. Don’t worry, caching systems periodically refresh their caches depending on how you set it up — so even constantly-changing web pages (like a blog post with comments) can be cached.

__Popular content management systems__ like WordPress and Drupal will have __static caching features__ that convert dynamically generated pages to static HTML files to reduce unnecessary server processing. For WordPress, check out [WP Super Cache](https://wordpress.org/plugins/wp-super-cache/) (one of the six critical WordPress plugins which, claimed by the author, enjoyed a improvement by 259.1% for content-heavy pages). Drupal has a page-caching feature in the core.

There are also __database caching and server-side scripts caching systems__ that you can install on your web server (if you have the ability to do so). For example, PHP has extensions called PHP accelerators that optimize performance through caching and various other methods; one example of a [PHP accelerator](http://en.wikipedia.org/wiki/PHP_accelerator) is APC. [Database caching](http://en.wikipedia.org/wiki/Database_caching) improves performance and scalability of your web applications by reducing the work associated with database read/write/access processes; __[memcached](http://www.memcached.org/)__, for example, caches frequently used database queries. 

#### 8. Load JavaScript at the End of Your Document

It’s best if you have your scripts loading at the end of the page rather than at the beginning. It allows for the browser to render everything before getting started with the JavaScript. This makes your web pages feel more responsive because the way JavaScript works is that it blocks anything below it from rendering until it has finished downloading. If possible, reference JavaScript right before the closing (body) tag of your HTML documents. To learn more, read about deferring the loading of JavaScript.

(to be continued...)
