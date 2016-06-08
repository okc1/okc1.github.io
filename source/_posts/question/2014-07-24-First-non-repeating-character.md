---
layout: post
title: "[Question] Find the first non-repeating character"
comments: true
category: Question
tags: [ unit test needed ]
---

### Question 

[link](http://www.geeksforgeeks.org/given-a-string-find-its-first-non-repeating-character/)

> Question One: Given a string, find the first non-repeating character in it

[link](http://www.geeksforgeeks.org/find-first-non-repeating-character-stream-characters/)

> Question Two: Given a stream of characters, find the first non-repeating character from stream. You need to tell the first non-repeating character in O(1) time at any moment.

### From a string

1. Scan the string from left to right and construct the count array.

1. Again, scan the string from left to right and check for count of each
 character, if you find an element who's count is 1, return it. 

__O(n) time__. 

The array is size of 128 if it's ASCII encoding. It can also be replaced with a HashMap if the length of the string is small. 

### From a stream of chars

__Use a DLL (doubly linked list), 1 count array and 1 DLL-node array__. Alternatively, the 2 arrays can be replaced with 2 HashMaps. 

In totally, one DLL and 2 array are used. __The DLL__ is used to get the sequence of non-repeating chars. __The 1st array__ is for char count, and __the 2nd array__ is for fast loop-up in the DLL. 

The detailed precedure: 

1. Create an empty DLL and 2 arrays: repeated[] and dllMap[]. 

1. To get the first non-repeating character, return the head of DLL.

1. Following are steps to process a new character 'x' in stream.

    1. If repeated[x] is false and dllMap[x] is NULL, append x to DLL and store it in dllMap[x]. 

    1. If repeated[x] is false and dllMap[x] is not NULL, get DLL node of x using dllMap[x] and remove the node. Set repeated[x] as true and optionally clear dllMap[x].

    1. If repeated[x] is true, ignore it. 

I didn't write code for this question. 
