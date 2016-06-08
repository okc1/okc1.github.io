---
layout: post
title: "[Design] How Google search works "
comments: true
category: Design

---

# Overview

Launched on Sep 15th, 1997

__60 trillion individual pages. 100 million GB data__. 

__40,000 search per second__, or 3 billion search per day. 

As of Feb 2015, 65% market share in US.

# 1. Crawl

Google crawl from 1 page to another using __[Googlebot](https://support.google.com/webmasters/answer/182072?vid=1-635765406868848825-432642872)__. It starts from previous urls crawled, or augmented with __[Sitemap data](https://en.wikipedia.org/wiki/Site_map)__

> __A sitemap__ is a list of pages of a web site accessible to crawlers or users. It can be either a document in any form used as a planning tool for Web design, or a Web page that lists the pages on a Web site, typically organized in hierarchical fashion.

# 2. Indexing 

Compile the data (key content tags, atrributes, like title tags, ALT attributes). Google don't process rich media or dynamic files. 

# 3. Algorithm

When search, pull all relevant results from the Index. 

Rank the result based on 200+ factors, one of which is the __[PageRank](https://en.wikipedia.org/wiki/PageRank)__ for a given page.

> __PageRank__ is the measure of the importance of a page based on the incoming links from other pages. In simple terms, each link to a page on your site from another site adds to your site's PageRank. 

> Not all links are equal: Google works hard to identify spam links. The best types of links are those that are given based on the quality of your content.

To rank higher, follow [Webmaster Guidelines](https://support.google.com/webmasters/answer/35769?vid=1-635765406868848825-432642872).
