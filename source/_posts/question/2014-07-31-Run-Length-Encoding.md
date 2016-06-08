---
layout: post
title: "[Question] Run-Length Encoding"
comments: true
category: Question

---

### Question 

[link](http://tech-queries.blogspot.sg/2008/11/run-length-encoding.html)

> You are given a string like "aaaabbbcc", do an in place conversion which write frequency of each charater(which come continuosly) with that character. 

> Example:
>
>input: aaabbbcc
>
>output: a3b2c2

### Solution

The most important point is __whether or not you find the special cases__, and did you clarify how to handle them. 

__First special case is only 1 character__, should you append a '1' or not. Note that this question requires 'in place' conversion. So '1' is not supposed to be appended after single-occurance character. This is really important to know, if the question does not specify. (though sometimes, the question asks you to apppend a '1', eg. [here](http://www.geeksforgeeks.org/run-length-encoding/)). 

__Second case is when occurance >= 10__. We could not simply append ('0' + numberOfOccurance), because the number could be 12. This is another very important case to take note. 

The code can be seen anywhere. 