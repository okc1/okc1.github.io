---
layout: post
title: "[LeetCode Plus] Lowest Common Ancestor of BST "
comments: true
category: leetcode_plus

---

### Question 

[link](http://leetcode.com/2011/07/lowest-common-ancestor-of-a-binary-search-tree.html)

<div class="entry bg-color bg-img font-color">
    <blockquote class="bg-color bg-img font-color">
        <p class="font-color bg-color bg-img">Given a binary search tree (BST), find the lowest common ancestor of two given nodes in the BST.</p>
    </blockquote>
    <p class="font-color bg-color bg-img"><span id="more-782" class="font-color"></span>
        <br>
    </p><pre class="bg-color bg-img font-color">        _______<span style="color: #990000;" class="font-color">6</span>______
       /              \
    ___<span style="color: #990000;" class="font-color">2</span>__          ___<span style="color: #990000;" class="font-color">8</span>__
   /      \        /      \
   <span style="color: #990000;" class="font-color">0</span>      _<span style="color: #990000;" class="font-color">4       7       9</span>
         /  \
         <span style="color: #990000;" class="font-color">3   5</span></pre>
    <p class="font-color bg-color bg-img">Using the above tree as an example, the lowest common ancestor (LCA) of nodes <span style="color: #990000;" class="font-color">2</span> and <span style="color: #990000;" class="font-color bg-color bg-img">8</span> is <span style="color: #990000;" class="font-color">6</span>. But how about LCA of nodes <span style="color: #990000;" class="font-color">2</span> and <span style="color: #990000;" class="font-color">4</span>? Should it be <span style="color: #990000;" class="font-color">6</span> or <span style="color: #990000;" class="font-color">2</span>?</p>
    <p class="font-color bg-color bg-img">According to the <a href="http://en.wikipedia.org/wiki/Least_common_ancestor" class="font-color">definition of LCA on  Wikipedia</a>: "The lowest common ancestor is defined between two nodes <em>v</em> and <em>w</em> as the lowest node in T that has both <em>v</em> and <em>w</em> as descendants (where we allow a node to be a descendant of itself)." Since a node can be a descendant of itself, the LCA of <span style="color: #990000;" class="font-color">2</span> and <span style="color: #990000;" class="font-color">4</span> should be <span style="color: #990000;" class="font-color">2</span>, according to this definition.</p>
    <p class="font-color bg-color bg-img"><strong>Hint:</strong>
        <br>A top-down walk from the root of the tree is enough.</p>
</div>

### Analysis 

__This question is the easiest of this series of questions__. I will quote the solution analysis.

> There’s only three cases you need to consider. 

    1. Both nodes are to the left of the tree.
    2. Both nodes are to the right of the tree.
    3. One node is on the left while the other is on the right. This node must be LCA. 
    4. Current node equals to one of the two nodes, this node must be the LCA. 

> The run time complexity is O(h), where h is the height of the BST. 

### Code

The code is not written by me. 

    Node *LCA(Node *root, Node *p, Node *q) {
      if (!root || !p || !q) return NULL;
      if (max(p->data, q->data) < root->data)
        return LCA(root->left, p, q);
      else if (min(p->data, q->data) > root->data)
        return LCA(root->right, p, q);
      else
        return root;
    }
