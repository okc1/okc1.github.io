---
layout: post
title: "[Google] Heap and BST conversion "
comments: true
category: q-google

---

### Question 1

[link](http://www.careercup.com/question?id=4281027)

> Convert a BST to max heap. 

### Solution 

The [second answer](http://www.careercup.com/question?id=4281027): 

> a simple (reversed) in-order traversal of the BST. It would produce a sorted array which is indeed a max-heap!

### Question 2

[link](http://stackoverflow.com/questions/14106821/converting-a-heap-to-a-bst-in-on-time)

> Converting a heap to a BST in O(n) time?

> possible? 

### Solution 

[Impossible](http://stackoverflow.com/a/14107362). Because otherwise, we can do this: 

1. Take an array and build the heap in O(n) time
1. Converting the heap to a BST in O(n) time (assuming) 
1. Walking the BST in O(n) time to get a sorted sequence.

Thus we sort array in O(n) time, it can't happen. 

Right way to do, is to repeatedly dequeueing maximum value from the BST, then generate the BST recursively (bottom-up approach). 
