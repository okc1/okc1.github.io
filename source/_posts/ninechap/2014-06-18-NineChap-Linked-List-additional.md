---
layout: post
title: "[NineChap 4.2] Linked List Additional"
comments: true
category: NineChap

---


## Question list

1. __[Union and Intersection of two Linked Lists]({% post_url /question/2014-06-17-Union-and-intersection-of-linked-list %})__

1. __[Insertion Sort List]({% post_url /leetcode/2014-05-30-Insertion-Sort-List %})__ - difficult

1. __[Flatten Binary Tree to Linked List]({% post_url /leetcode/2014-05-28-Flatten-Binary-Tree-to-Linked-List %})__

1. __[Convert Sorted List to Binary Search Tree]({% post_url /leetcode/2014-05-26-Convert-Sorted-List-to-Binary-Search-Tree %})__

1. __[Rotate List]({% post_url /leetcode/2014-05-19-Rotate-List %})__

1. __[Remove Nth Node From End of List]({% post_url /leetcode/2014-05-02-Remove-Nth-Node-From-End-of-List %})__

1. __[LRU Cache ]({% post_url /leetcode/2014-06-03-LRU-Cache %})__

1. __[Reverse Nodes in k-Groups]({% post_url /leetcode/2014-05-11-Reverse-Nodes-in-k-Group %})__

1. __[Swap Nodes in Pairs]({% post_url /leetcode/2014-05-09-Swap-Nodes-in-Pairs %})__

## Code

__Union and Intersection of two Linked Lists__

Think about the idea only. 

__Insertion Sort List__

    public ListNode insertionSortList(ListNode head) {
        if (head == null) {
            return null;
        }
        ListNode dummy = new ListNode(0);
        ListNode cur = head;
        while (cur != null) {
            // insert cur into correct pos
            ListNode pos = dummy;
            while (pos.next != null && pos.next.val < cur.val) {
                pos = pos.next;
            }
            ListNode temp = cur.next;
            cur.next = pos.next;
            pos.next = cur;
            cur = temp;
        }
        return dummy.next;
    }

__Flatten Binary Tree to Linked List__

I forgot to set "root.left = null" again, which result in long-time debugging. This is a very common and very silly mistake that I really should avoid. 

    public void flatten(TreeNode root) {
        root = helper(root);
    }
    
    private TreeNode helper(TreeNode node) {
        if (node == null) {
            return null;
        } else if (node.left == null && node.right == null) {
            return node;
        } else if (node.left == null) {
            return helper(node.right);
        } else if (node.right == null) {
            node.right = node.left;
            node.left = null;
            return helper(node.right);
        } else {
            TreeNode tempRight = node.right;
            node.right = node.left;
            node.left = null;
            TreeNode leftTail = helper(node.right);
            leftTail.right = tempRight;
            return helper(tempRight);
        }
    }

__Convert Sorted List to Binary Search Tree__

This is the Mock Interview question. My solution is: 

    public TreeNode sortedListToBST(ListNode listHead) {
        if (listHead == null) {
            return null;
        }
        if (listHead.next == null) {
            return new TreeNode(listHead.val);
        }
        ListNode listFirstHalf = listHead;
        ListNode listPreMid = findMiddle(listHead);
        ListNode listSecondHalf = null;
        if (listPreMid.next != null) {
            listSecondHalf = listPreMid.next.next;
        }
        TreeNode head = new TreeNode(listPreMid.next.val);
        listPreMid.next = null;
        head.left = sortedListToBST(listFirstHalf);
        head.right = sortedListToBST(listSecondHalf);
        return head;
    }
    
    private ListNode findMiddle(ListNode listHead) {
        if (listHead == null) {
            return null;
        }
        ListNode slow = listHead;
        ListNode fast = listHead.next;
        while (fast != null && fast.next != null&& fast.next.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }

This is not a good answer, cuz I have to findMid in each recursion. 

The best solution is, use a global variable and 2 numbers to simplify this process. Code: 

	ListNode cur = null;
	
    public TreeNode sortedListToBST(ListNode head) {
		if (head == null) {
			return null;
		}
		cur = head;
		int k = 0;
		ListNode p = head;
		while (p != null) {
			k++;
			p = p.next;
		}
		return build(0, k - 1);
    }
	
	private TreeNode build(int start, int end) {
		if (start > end) {
			return null;
		}
		int mid = start + (end - start) / 2;
		TreeNode leftBranch = build(start, mid - 1);
		TreeNode head = new TreeNode(cur.val);
		cur = cur.next;
		head.left = leftBranch;
		head.right = build(mid + 1, end);
		return head;
	}

__Rotate List__

Naive solution: 

    public ListNode rotateRight(ListNode head, int n) {
        if (head == null) {
            return null;
        }
        ListNode p = head;
        for (int i = 0; i < n; i++) {
            if (p.next == null) {
                p = head;
            } else {
                p = p.next;
            }
        }
		ListNode q = head;
		while (p.next != null) {
			p = p.next;
			q = q.next;
		}
		p.next = head;
		ListNode newHead = q.next;
		q.next = null;
		return newHead;
    }

Make a circular list: 

    public ListNode rotateRight(ListNode head, int n) {
        if (head == null) {
            return null;
        }
		ListNode p = head;
		int k = 1;
		while (p.next != null) {
			k++;
			p = p.next;
		}
		p.next = head;
		int steps = k - (n % k);
		for (int i = 0; i < steps; i++) {
			p = p.next;
		}
		head = p.next;
		p.next = null;
		return head;
    }

__Remove Nth Node From End of List__

    public ListNode removeNthFromEnd(ListNode head, int n) {
        if (head == null || n == 0) {
			return null;
		}
		ListNode dummy = new ListNode(0);
		dummy.next = head;
		ListNode right = dummy;
		for (int i = 0; i < n; i++) {
			right = right.next;
		}
		ListNode left = dummy;
		while (right.next != null) {
			left = left.next;
			right = right.next;
		}
		left.next = left.next.next;
		return dummy.next;
    }

__LRU Cache__

I solved it in the original post. 

__Reverse Nodes in k-Groups__

    public ListNode reverseKGroup(ListNode head, int k) {
        ListNode p = head;
        int count = 0;
        while (p != null) {
            p = p.next;
            count++;
        }
        return helper(head, k, count);
    }
    
    public ListNode helper(ListNode head, int k, int count) {
        if (head == null || k < 1 || count < k) {
            return head;
        }
        ListNode result = null;
        ListNode cur = head;
        for (int i = 0; i < k; i++) {
            if (cur == null) break;
            ListNode temp = cur.next;
            cur.next = result;
            result = cur;
            cur = temp;
        }
        head.next = helper(cur, k, count - k);
        return result;
    }

__Swap Nodes in Pairs__

    public ListNode swapPairs(ListNode head) {
        if (head == null || head.next == null) {
            return head;
        }
        ListNode result = head.next;
        ListNode temp = head.next.next;
        result.next = head;
        head.next = swapPairs(temp);
        return result;
    }
