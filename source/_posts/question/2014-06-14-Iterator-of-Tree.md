---
layout: post
title: "[Question] Iterator of Binary Search Tree"
comments: true
category: Question
tags: [  ]
---


### Question 

> Implement a iterator for a binary search tree

__Related question__: [Binary Tree Inorder Traversal]({% post_url /leetcode/2014-05-24-Binary-Tree-Inorder-Traversal %})

### Analysis 

First of all, what is an iterator in Java? 

> Java has a commonly used Iterator interface.
>
> It is usually used like this:

    Iterator e = container.iterator();  
    while (e.hasNext()) {
        System.out.println(e.next());
    }

The source code of Iterator interface: 

    public interface Iterator<E> {
        boolean hasNext();
        E next();
        void remove();
    }

In this post, we will only implement next(), because Tree node deletion is covered in another post, and it's not easy. 

The most standard way is to do an inorder traversal (by storing a pointer to the next node). The only difference is iterator is 1 step at a time. If you cannot write inorder traversal without using recursion, [learn it first]({% post_url /leetcode/2014-05-24-Binary-Tree-Inorder-Traversal %}). The solution of iterator is available from [this blog](http://manbroski.blogspot.sg/2011/11/iterator-for-binary-search-tree.html), although he made some small syntax errors. 

### Code

    public class BinaryTreeIterator {

        private Stack<TreeNode> stack = new Stack<TreeNode>();

        public BinaryTreeIterator(TreeNode root) {
            if (root == null) {
                throw new NoSuchElementException("Empty tree");
            }
            while (root != null) {
                stack.push(root);
                root = root.left;
            }
        }

        public boolean hasNext() {
            return !stack.isEmpty();
        }

        public TreeNode next() {
            TreeNode top = stack.pop();
            TreeNode right = top.right;
            while (right != null) {
                stack.push(right);
                right = right.left;
            }
            return top;
        }
    }