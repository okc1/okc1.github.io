---
layout: post
title: "[Google] Transform a unbalanced tree into balanced tree "
comments: true
category: q-google

---

### Question 

[link](http://www.careercup.com/question?id=5979667)

> How to serialize strings and pass it over the network and de-serialize the string? 

> The string may contain __any possible character__ out of 256 valid characters. 

### Solution 

The difficulty is how to __differentiate between data (string) and metadata__. Some interesting ideas:

1. XML
2. message with header + body

The best is the [top answer](http://www.careercup.com/question?id=5979667): 

> I think that a good answer is to send the length of the string in bytes (coded for example as a 4 bytes unsigned integer) followed by the list of bytes, one per char. 

> The receiver reads the first 4 bytes and understand the string length (let says L), then it reads the following L bytes and build the string. 

### Code

eg. 5hello 5world 2my 4name 2is
