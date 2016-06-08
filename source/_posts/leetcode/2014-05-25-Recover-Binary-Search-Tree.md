---
layout: post
title: "[LeetCode 99] Recover Binary Search Tree"
comments: true
category: Leetcode

---

### Question 
[link](https://oj.leetcode.com/problems/recover-binary-search-tree/)

<div class="question-content">
            <p></p><p>
Two elements of a binary search tree (BST) are swapped by mistake.</p>

<p>Recover the tree without changing its structure.
</p>

<b>Note:</b><br>
A solution using O(<i>n</i>) space is pretty straight forward. Could you devise a constant space solution?
<p></p>

<p></p>
</div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="lime">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is one of the most difficult questions that I have solved__.

The question can be solved using 2 pointers to point to the 2 misplaced nodes, and swap them. I solved the problem with this approach, and I found a good explanation [here](http://chaoren.is-programmer.com/posts/42931.html). 

>Only two variables (first, second) are enough to record nodes to be exchanged. 
>
>If there's only one descending order pair (e.g. 20, 10, 30, 40, 50), use first & second to record it. 
>
>If there are two descending order pairs (e.g. 10, 40, 30, 20, 50 or 50, 20, 30, 40, 10), use the smaller number in second pair to update variable 'second'. 
>
>In the end, swap first and second.

This is a popular solution on the Internet, which __uses O(1) space, plus average case O(lgn) stack space__ (because recursion always incur stack usage). So this solution is actually not fulfilling the requirements. 

> 中序遍历二叉树的空间复杂度是O(logN) on average case

__So finally I found a solution with constent space, and it's using Treaded Binary Tree again__! Look below for details. 

### Solution

[This](http://www.geeksforgeeks.org/inorder-tree-traversal-without-recursion-and-without-stack/) is a systematic analysis of __Morris Traversal__ based on __Threaded Binary Tree__. 

__A solution of using Morris Traversal is explained [here](http://www.cnblogs.com/TenosDoIt/p/3445682.html)__. Don't worry about the tree structure being changed, because it's reverted back after the traversal. 

> 算法2：为了满足O(1)空间复杂度，我们就要使用非递归且不使用栈的中序遍历算法，在leetcode另一个题目Binary Tree Inorder Traversal中，我们提到了Morris Traversal中序遍历算法，它既没有递归，也没有使用栈，而是用了线索二叉树的思想，用闲置的右节点指向中序序列中该节点的后缀，遍历后再恢复树的原始指针。其主要算法步骤如下：

> 重复以下1、2直到当前节点为空。 

__[Another person](http://fisherlei.blogspot.sg/2012/12/leetcode-recover-binary-search-tree.html)__ have a very good (maybe better) English version of analysis and code: 

    1. Initialize current as root 
    2. While current is not NULL
       If current does not have left child
          a) Print current’s data
          b) Go to the right, i.e., current = current-&gt;right
       Else
          a) Make current as right child of the rightmost node in current's left subtree
          b) Go to this left child, i.e., current = current-&gt;left

### Code

__First, my code (2 pointer solution)__

	TreeNode first = null, second = null;
	TreeNode pre = new TreeNode(Integer.MIN_VALUE);

	public void recoverTree(TreeNode root) {
        helper(root);
        // now first and second are both found
        int temp = first.val;
        first.val = second.val;
        second.val = temp;
    }
    
    private void helper(TreeNode root) {
        if (root == null) return;
        helper(root.left);
        if (pre.val > root.val) {
            if (first == null) {
                first = pre;
                second = root;
            }
            else second = root;
        }
        pre = root;
        helper(root.right);
    }

__Second, real O(1) space solution__ using Threaded Binary Tree (i.e. Morris Traversal) in C++. I could not memorize this code. 

    void recoverTree(TreeNode *root) {
           TreeNode *f1=NULL, *f2=NULL;
           TreeNode  *current,*pre, *parent=NULL;

           if(root == NULL)
                 return;
           bool found = false;
           current = root;
           while(current != NULL)
           {                
                 if(current->left == NULL)
                 {
                        if(parent && parent->val > current->val)
                        {
                               if(!found)
                               {
                                     f1 = parent;
                                     found = true;
                               }
                               f2 = current;
                        }
                        parent = current;
                        current = current->right;     
                 }   
                 else
                 {
                        /* Find the inorder predecessor of current */
                        pre = current->left;
                        while(pre->right != NULL && pre->right != current)
                               pre = pre->right;

                        /* Make current as right child of its inorder predecessor */
                        if(pre->right == NULL)
                        {
                               pre->right = current;
                               current = current->left;
                        }

                        /* Revert the changes made in if part to restore the original
                        tree i.e., fix the right child of predecssor */  
                        else
                        {
                               pre->right = NULL;
                               if(parent->val > current->val)
                               {
                                     if(!found)
                                     {
                                            f1 = parent;       
                                            found = true;
                                     }
                                     f2 = current;
                               }
                               parent = current;
                               current = current->right;     
                        } /* End of if condition pre->right == NULL */
                 } /* End of if condition current->left == NULL*/
           } /* End of while */

           if(f1 && f2)
                 swap(f1->val, f2->val);
    }
