---
layout: post
title: "[NineChap 3.3] Binary Search Tree"
comments: true
category: NineChap

---


## Question list

__BST__

1. __[Validate Binary Search Tree]({% post_url /leetcode/2014-05-26-Validate-Binary-Search-Tree %})__

1. __[Insert a Node in Binary Search Tree]({% post_url /design/2014-06-11-BST-insert-and-delete %})__

1. __[Delete a Node in Binary Search Tree]({% post_url /design/2014-06-11-BST-insert-and-delete %})__

1. __[Search Range in a Binary Search Tree]({% post_url /question/2014-06-13-Search-range-BST-trim-BST %})__

__Additional__

1. __[Recover Binary Search Tree]({% post_url /leetcode/2014-05-25-Recover-Binary-Search-Tree %})__ - used global variable

1. __[Convert Sorted Array to Binary Search Tree]({% post_url /leetcode/2014-05-26-Convert-Sorted-Array-to-Binary-Search-Tree %})__

1. __[Convert Sorted List to Binary Search Tree]({% post_url /leetcode/2014-05-26-Convert-Sorted-List-to-Binary-Search-Tree %})__ - used global variable

## Code

__Validate Binary Search Tree__

    public boolean isValidBST(TreeNode root) {
        return validate(root, Integer.MIN_VALUE, Integer.MAX_VALUE);
    }

	private boolean validate(TreeNode node, int min, int max) {
		if (node == null) {
			return true;
		}
		if (node.val <= min || max <= node.val) {
			return false;
		}
		return validate(node.left, min, node.val) & validate(node.right, node.val, max);
	}

__Insert a Node in Binary Search Tree__ and __Delete a Node in Binary Search Tree__ are written in a new post. 

__Search Range in a Binary Search Tree__

There is a new post for this. 

__Recover Binary Search Tree__

    // 3 global variables used
    TreeNode first = null;
    TreeNode second = null; 
    TreeNode current = null;
    
    public void recoverTree(TreeNode root) {
        traverse(root);
        if (first != null) {
            int temp = first.val;
            first.val = second.val;
            second.val = temp;
        }
    }
    
    public void traverse(TreeNode root) {
        if (root == null) {
            return;
        }
        traverse(root.left);
        // inorder traversal
        if (current != null && current.val > root.val) {
            if (first == null) {
                first = current;
            }
            second = root;
        }
        current = root;
        traverse(root.right);
    }

__Convert Sorted Array to Binary Search Tree__

    public TreeNode sortedArrayToBST(int[] num) {
        if (num == null || num.length == 0) {
			return null;
		}
		return build(num, 0, num.length - 1);
    }

	private TreeNode build(int[] num, int start, int end) {
		if (start > end) {
			return null;
		}
		int mid = start + (end - start) / 2;
		TreeNode head = new TreeNode(num[mid]);
		head.left = build(num, start, mid - 1);
		head.right = build(num, mid + 1, end);
		return head;
	}

__Convert Sorted List to Binary Search Tree__ - note that this solution uses 1 global variable

	ListNode cur = null;
	
    public TreeNode sortedListToBST(ListNode head) {
		// count total length of the list 
		ListNode p = head;
		int count = 0;
		while (p != null) {
			p = p.next;
			count++;
		}
		// start to traverse the tree and fill in data
		cur = head;
		return build(0, count - 1);
    }
	
	private TreeNode build(int start, int end) {
		if (start > end) {
			return null;
		}
		int mid = start + (end - start) / 2;
		TreeNode head = new TreeNode(0);
		head.left = build(start, mid - 1);
		head.val = cur.val;
		cur = cur.next;
		head.right = build(mid + 1, end);
		return head;
	}
