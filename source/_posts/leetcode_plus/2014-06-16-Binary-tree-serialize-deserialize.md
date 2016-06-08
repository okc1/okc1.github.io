---
layout: post
title: "[LeetCode Plus] Binary Tree Serialize and Deserialize"
comments: true
category: leetcode_plus
tags: [ unit test needed ]
---


### Question 

[link1](http://leetcode.com/2010/09/serializationdeserialization-of-binary.html), [link2](http://leetcode.com/2010/09/saving-binary-search-tree-to-file.html).

> Variant 1: Given a Binary Search Tree, serialize and deserialize it.

> Variant 2: Given a Binary Tree, serialize and deserialize it.

### Variant 1 - Binary search tree

__We must only use pre-order__. 

Think about why, or read [link1](http://leetcode.com/2010/09/serializationdeserialization-of-binary.html). So, serialization is simple - preorder traversal. 

The desecialization would make use of the first element, and range validation method. This is very similar to another question 'validate BST'. Rmb the key is: 

> Each time we add a number, we also pass the valid range within which the number can lie between. 

#### Code

The code is concise, but may not be easy to write: 

    void readBSTHelper(int min, int max, int &insertVal,
                       BinaryTree *&p, ifstream &fin) {
      if (insertVal > min && insertVal < max) {
        int val = insertVal;
        p = new BinaryTree(val);
        if (fin >> insertVal) {
          readBSTHelper(min, val, insertVal, p->left, fin);
          readBSTHelper(val, max, insertVal, p->right, fin);
        }
      }
    }

    void readBST(BinaryTree *&root, ifstream &fin) {
      int val;
      fin >> val;
      readBSTHelper(INT_MIN, INT_MAX, val, root, fin);
    }

### Variant 2 - Binary tree

For binary tree, we could not use above solution any more. We must use some NULL pointers to fill in empty slots. For this variant, __pre-order and level-order both would work__. 

Then which of these 2 is a better choice?

<pre>
   1
  / \
 2   3
</pre>

> Given the tree above: 
>
> The pre-order serialization is: {1, 2, #, #, 3, #, #}
>
> The level-order serialization is: {1, 2, 3}
>
> We can see that level-order is a better idea, because last level null pointers need not be handled. 

#### Code (preorder)

The serializaion is a simple traversal. 

    void writeBinaryTree(BinaryTree *p, ostream &out) {
      if (!p) {
        out << "# ";
      } else {
        out << p->data << " ";
        writeBinaryTree(p->left, out);
        writeBinaryTree(p->right, out);
      }
    }

The deserialization is a little bit like "convert linked list to balanced tree" (where we use first element of the list as root of the tree). 

    void readBinaryTree(BinaryTree *&p, ifstream &fin) {
      int token;
      bool isNumber;
      if (!readNextToken(token, fin, isNumber)) 
        return;
      if (isNumber) {
        p = new BinaryTree(token);
        readBinaryTree(p->left, fin);
        readBinaryTree(p->right, fin);
      }
    }

I did not find any code for level-order, but it's similar to 'level-order traversal'. 

### One more thing

A Binary Search Tree (BST) is useful for storing phone book records in a memory limited device, such as a cell phone. The records are always maintained in sorted order, inserting and deleting a record takes O(lg n) time (slower than linked list, but much better than array). 

### One more one-more-thing

__This post we use # as a sentinel__. There is also __[another idea](http://stackoverflow.com/a/15044868) of doing both Inorder and Preorder traversal__ to searialize the tree data, and use the solution to "Construct Binary Tree from Preorder and Inorder" to deserialize it. 
