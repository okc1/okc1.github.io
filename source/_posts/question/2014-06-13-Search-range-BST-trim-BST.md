---
layout: post
title: "[Question] Search Range in BST (Trim a BST)"
comments: true
category: Question
tags: [ unit test needed ]
---


### Question 

[link](http://www.ardendertat.com/2012/01/17/programming-interview-questions-26-trim-binary-search-tree/)

> Given the root of a binary search tree and 2 numbers min and max, trim the tree such that all the numbers in the new tree are between min and max (inclusive). The resulting tree should still be a valid binary search tree. 

Input: 

{% img middle /assets/images/search-range-input.png %}

With min value as 5 and max value as 13, the output is:

{% img middle /assets/images/search-range-output.png %}

### Analysis 

There is a good analysis from [geeksforgeeks](http://www.geeksforgeeks.org/print-bst-keys-in-the-given-range/): 

>1. If value of root’s key is greater than k1, then recursively call in left subtree.
>2. If value of root’s key is in range, then print the root’s key.
>3. If value of root’s key is smaller than k2, then recursively call in right subtree.

Another great solution is from [Arden Dertat](http://www.ardendertat.com/2012/01/17/programming-interview-questions-26-trim-binary-search-tree/).

### Code

First code, from geeksforgeeks - print the result instead of return.

    void Print(struct node *root, int k1, int k2)
    {
       if ( NULL == root )
          return;
       if ( k1 < root->data )
         Print(root->left, k1, k2);
       if ( k1 <= root->data && k2 >= root->data )
         printf("%d ", root->data );
       if ( k2 > root->data )
         Print(root->right, k1, k2);
    }

Second code from Arden:

    def trimBST(tree, minVal, maxVal): 
        if not tree: 
            return 
        tree.left=trimBST(tree.left, minVal, maxVal) 
        tree.right=trimBST(tree.right, minVal, maxVal) 
        if minVal<=tree.val<=maxVal: 
            return tree 
        if tree.val<minVal: 
            return tree.right 
        if tree.val>maxVal: 
            return tree.left
