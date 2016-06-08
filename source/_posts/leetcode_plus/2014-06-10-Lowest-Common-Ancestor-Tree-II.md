---
layout: post
title: "[LeetCode Plus] Lowest Common Ancestor of Binary Tree (II)"
comments: true
category: leetcode_plus

---

### Question 

[link](http://leetcode.com/2011/07/lowest-common-ancestor-of-a-binary-tree-part-ii.html)

<div class="entry bg-color bg-img font-color">
    <blockquote>
        <p class="font-color">Given a binary tree, find the lowest common ancestor of two given nodes in the tree. Each node contains a parent pointer which links to its parent.</p>
    </blockquote>
    <p class="font-color bg-color bg-img"><span id="more-797" class="font-color"></span>
        <br> <strong><span style="color: red;" class="font-color">Note:</span></strong>
        <br>This is Part II of Lowest Common Ancestor of a Binary Tree. If you need to find the lowest common ancestor without parent pointers, please read <a href="http://www.leetcode.com/2011/07/lowest-common-ancestor-of-a-binary-tree-part-i.html" class="font-color">Lowest Common Ancestor of a Binary Tree Part I</a>.
        <br>
    </p><pre>        _______<span style="color: #990000;" class="font-color">3</span>______
       /              \
    ___<span style="color: #990000;" class="font-color">5</span>__          ___<span style="color: #990000;" class="font-color">1</span>__
   /      \        /      \
   <span style="color: #990000;" class="font-color">6</span>      _<span style="color: #990000;" class="font-color">2       0       8</span>
         /  \
         <span style="color: #990000;" class="font-color">7   4</span></pre>
    <p class="font-color">If you are not so sure about the definition of lowest common ancestor (LCA), please refer to my previous post: <a href="http://www.leetcode.com/2011/07/lowest-common-ancestor-of-a-binary-search-tree.html" class="font-color">Lowest Common Ancestor of a Binary Search Tree (BST)</a> or the definition of LCA <a href="http://en.wikipedia.org/wiki/Lowest_common_ancestor" class="font-color">here</a>. Using the tree above as an example, the LCA of nodes <span style="color: #990000;" class="font-color">5</span> and <span style="color: #990000;" class="font-color">1</span> is <span style="color: #990000;" class="font-color">3</span>. Please note that LCA for nodes <span style="color: #990000;" class="font-color">5</span> and <span style="color: #990000;" class="font-color">4</span> is <span style="color: #990000;" class="font-color">5</span>.</p>
    <p class="font-color">In my last post: <a href="http://www.leetcode.com/2011/07/lowest-common-ancestor-of-a-binary-tree-part-i.html" class="font-color">Lowest Common Ancestor of a Binary Tree Part I</a>, we have devised a recursive solution which finds the LCA in O(<em>n</em>) time. If each node has a pointer that link to its parent, could we devise a better solution?</p>
    <p class="font-color"><strong>Hint:</strong>
        <br>No recursion is needed. There is an easy solution which uses extra space. Could you eliminate the need of extra space?</p>
</div>

### Analysis 

__If have parent pointer, we do not wish to use extra space for the solution__. 

1. Find the height of both nodes (from the head)
2. By calculating the height difference, move the lower nodes up (follow the parent path) to the same level as the other node. 
3. Two nodes move up together until they meet. 
4. This solution requires no extra space.

Here is __a very similar question: [Intersection of 2 LinkedList](http://www.geeksforgeeks.org/write-a-function-to-get-the-intersection-point-of-two-linked-lists/)__. 

### Code
 
    // As root->parent is NULL, we don't need to pass root in.
    Node *LCA(Node *p, Node *q) {
      int h1 = getHeight(p);
      int h2 = getHeight(q);
      // swap both nodes in case p is deeper than q.
      if (h1 > h2) {
        swap(h1, h2);
        swap(p, q);
      }
      // invariant: h1 <= h2.
      int dh = h2 - h1;
      for (int h = 0; h < dh; h++)
        q = q->parent;
      while (p && q) {
        if (p == q) return p;
        p = p->parent;
        q = q->parent;
      }
      return NULL;  // p and q are not in the same tree
    }

    int getHeight(Node *p) {
      int height = 0;
      while (p) {
        height++;
        p = p->parent;
      }
      return height;
    }