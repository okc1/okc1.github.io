---
layout: post
title: "[Google] Max prodcut of strings that have no common char "
comments: true
category: q-google

---

### Question 

[link](http://www.mitbbs.com/article_t1/JobHunting/32868775_0_1.html)

> Given a dictionary of wrods,find the pair of word with following property: 

> 1. the two word don't have same letter. 
>
> 2. the multiple of the two word's length is maximum. 

> I give a simple O(n*n*k)(k is the average length of word) method.but i think there will be better one.

### Solution 

[Best answer](http://www.careercup.com/question?id=4951409057333248) suggest as top comment: 

> Assuming the word is A-Z/a-z only, use a bitmap to set which letters it contains. 

> e.g. ca => 000....101 
>
> bb => 000...010 

This is called __Bitmask__ of string. Read __[Question] Check string with no common letters (Bitmask)__.

Then: 

> Iterate over the words in decreasing order of length. 

> for each pair of words, AND the bitmaps. 

> Return the first pair that gives a 0 result. 

> This should be n*k + n*n

#### Be cautious

For the second part of the solution above, is this code going to work? 

    Arrays.sort(strs) in descending order;
    for (int i = 0; i < strs.length; i++) {
        for (int j = 0; j < i; j++) {
            if (strs[i].bitmask & strs[j].bitmask == 0) {
                // this pair do not have common char
                // since strs in descending order, and i, j start from 0
                // the product of length should be max
                return i + ' ' + j;
            }
        }
    }

Well, this is wrong. For example: {"ababa", "aaa", "bbb", "cc"}, if we do longest-string to shorest-string, we would return "aaa", "bbb" immediately when we found it. __However, 5 * 2 > 3 * 3__. 

So, we have to find largest product using max-heap, like we did in __[Google] Top N Values From Sum of 2 Arrays__, "pop 1 and push 2". 

### Another solution

__DP__: for each string, find the reversed set of char, and then find the max string using the reversed set. This idea is great, too, but less intuitive. 

It is explained [here](http://qr.ae/BYGHK). 

### Code

not written
