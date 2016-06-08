---
layout: post
title: "[ItInt5] Number of Valid Trees Given Preorder and Postorder "
comments: true
category: Question
tags: [ ItInt5 ]
---

### Question 

[link](http://www.itint5.com/oj/#28)

> 对于包含n个结点的二叉树（树中结点编号从1到n），已知前序和后序遍历序列，我们知道不一定能唯一的恢复这棵树。请计算出满足条件的二叉树的总数。

> Example

    前序遍历序列preorder：1 2
    后序遍历序列postorder：2 1

    一共有2棵满足条件的二叉树：
        1       1
       /         \
      2           2

### Solution

> 先看两种遍历的性质:

> pre-order: root, left *************, right #########
>
> post-order: **************left, ########right, root

> 所以 pre-order 的第一个元素一定等于 post-order 的最后一个元素. 然后在post-order中由前往后找, 找出等于pre-oder[left]的位置 p. 

> 1. 如果 p 位置不是倒数第二个, fine, 对左右子树递归__调用后用乘法原理__.

> 1. 如果 p 是倒数第二个, 说明either left branch or right branch为空, return的值就是 __2 * 递归调用非空子树__.

[ref](http://www.itint5.com/discuss/94/%E8%AF%B7%E5%A4%A7%E5%AE%B6%E6%8F%90%E4%B8%80%E4%BA%9B%E6%94%B9%E8%BF%9B%E6%84%8F%E8%A7%81)

### Code

__not written by me__. This code is REALLY 叼炸天。

    int helper(vector<int>& preorder, vector<int>& posorder, 
             int i1, int j1, int i2, int j2){
        if(i1 == j1) return 1;
        if(preorder[i1+1] == posorder[j2-1]){
            return 2*helper(preorder, posorder, i1+1, j1, i2, j2-1);
        }
        int k = i2;
        while(posorder[k] != preorder[i1+1]){ k++; }
        return helper(preorder, posorder, i1+1,i1+1+k-i2 ,i2 , k)
             * helper(preorder, posorder, i1+2+k-i2, j1, k+1, j2-1);
    }

    int countValidTrees(vector<int>& preorder, vector<int>& posorder) {
        int n = preorder.size();
        return helper(preorder, posorder, 0, n-1, 0, n-1);
    }
