---
layout: post
title: "[NineChap 3.4] Binary Tree Additional"
comments: true
category: NineChap

---


These are some additional questions that are not covered in previous NineChap posts. Some questions are non-standard and difficult to solve, and some are not found in OJ websites. But these are real questions that has been asked during interviews. 

## Question list

1. __[Binary Search Tree find upper/lower bound]({% post_url /question/2014-06-15-BST-find-upper-lower-bound %})__

1. __[Implement iterator of Binary Search Tree]({% post_url /question/2014-06-14-Iterator-of-Tree %})__

1. __[Binary Tree Serialize and Deserialize]({% post_url /leetcode_plus/2014-06-16-Binary-tree-serialize-deserialize %})__

1. __[Populating Next Right Pointers in Each Node]({% post_url /leetcode/2014-05-27-Populating-Next-Right-Pointers-in-Each-Node %})__

1. __[Populating Next Right Pointers in Each Node II]({% post_url /leetcode/2014-05-27-Populating-Next-Right-Pointers-in-Each-Node-II %})__ - difficult

1. __[Symmetric Tree]({% post_url /leetcode/2014-05-26-Symmetric-Tree %})__

1. __[Same Tree]({% post_url /leetcode/2014-05-25-Same-Tree %})__

## Code

__Binary Search Tree find upper/lower bound__

Find the new post.

__Implement iterator of Binary Search Tree__

Find the new post.

__Binary Tree Serialize and Deserialize__

Find the new post.

__Populating Next Right Pointers in Each Node__

    public void connect(TreeLinkNode root) {
		TreeLinkNode dummy = new TreeLinkNode(0);
		dummy.left = root;
		helper(dummy, root);
    }
	
	private void helper(TreeLinkNode parent, TreeLinkNode child) {
		if (child == null) {
			return;
		}
		if (child == parent.left) {
			child.next = parent.right;
		} else if (child == parent.right) {
			if (parent.next != null) {
				child.next = parent.next.left;
			}
		}
		helper(child, child.left);
		helper(child, child.right);
	}

__Populating Next Right Pointers in Each Node II__

This is a very tricky variant of DFS where the left sub-tree is making use of right sub-tree. I did not solve it even at second time. 

    public void connect(TreeLinkNode root) {
        if (root == null) return;
        if (root.left == null && root.right == null) return;
        TreeLinkNode levelNext = root.next;
        TreeLinkNode lowerNext = null;
        while (levelNext != null && lowerNext == null) {
            if (levelNext.left != null) {
                lowerNext = levelNext.left;
                break;
            } else if (levelNext.right != null) {
                lowerNext = levelNext.right;
                break;
            } else {
                // if there is no child node of levelNext
                levelNext = levelNext.next;
            }
        }
        if (root.left == null) {
            root.right.next = lowerNext;
        } else if (root.right == null) {
            root.left.next = lowerNext;
        } else {
            root.left.next = root.right;
            root.right.next = lowerNext;
        }
        connect(root.right);
        connect(root.left);
    }

__Symmetric Tree__

    public boolean isSymmetric(TreeNode root) {
        if (root == null) {
			return true;
		}
		return mirror(root.left, root.right);
    }
	
	private boolean mirror(TreeNode left, TreeNode right) {
		if (left == null && right == null) {
			return true;
		}
		if (left == null || right == null) {
			return false;
		}
		return (left.val == right.val) 
			& mirror(left.left, right.right)
			& mirror(left.right, right.left);
	}

__Same Tree__

    public boolean isSameTree(TreeNode left, TreeNode right) {
		if (left == null && right == null) {
			return true;
		}
		if (left == null || right == null) {
			return false;
		}
		return (left.val == right.val) 
			& isSameTree(left.left, right.left)
			& isSameTree(left.right, right.right);
	}
