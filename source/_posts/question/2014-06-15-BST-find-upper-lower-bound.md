---
layout: post
title: "[Question] Binary Search Tree find upper/lower bound"
comments: true
category: Question
tags: [ unit test needed ]
---


### Question 

> Given a BST, find the node that is larger/smaller than particular number 

Or the question can be: 

> Given a binary search tree and a value k, please find a node in the binary search tree whose value is closest to k. [link](http://codercareer.blogspot.sg/2013/03/no-45-closest-node-in-binary-search-tree_2.html)

### Analysis 

__This post is based on the second question above__.

1. Traverse the tree top-down. 
2. While traversing, record values that are closer to target than previously-found value. 
3. If found, the target, break and return. [source](http://stackoverflow.com/a/6209372)

### Code

From [this post](http://codercareer.blogspot.sg/2013/03/no-45-closest-node-in-binary-search-tree_2.html).

    BinaryTreeNode* getClosestNode(BinaryTreeNode* pRoot, int value)
    {
        BinaryTreeNode* pClosest = NULL;
        int minDistance = 0x7FFFFFFF;
        BinaryTreeNode* pNode = pRoot;
        while(pNode != NULL){
            int distance = abs(pNode->m_nValue - value);
            if(distance < minDistance){
                minDistance = distance;
                pClosest = pNode;
            }

            if(distance == 0)
                break;

            if(pNode->m_nValue > value)
                pNode = pNode->m_pLeft;
            else if(pNode->m_nValue < value)
                pNode = pNode->m_pRight;
        }

        return pClosest;
    }