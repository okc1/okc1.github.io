---
layout: post
title: "[NineChap 3.2] Binary Tree BFS"
comments: true
category: NineChap

---


## Template (BFS)

BFS can be implemented using either 2 queues (replacing) or 1 queue. Of course 1 queue is better. 

[link](http://answer.ninechapter.com/solutions/bfs-template/)

    public ArrayList<ArrayList<Integer>> levelOrder(TreeNode root) {
        ArrayList result = new ArrayList();
        
        if (root == null)
            return result;
            
        Queue<TreeNode> queue = new LinkedList<TreeNode>();
        queue.offer(root);
        
        while (!queue.isEmpty()) {
            ArrayList<Integer> level = new ArrayList<Integer>(); // important
            int size = queue.size();
            for (int i = 0; i < size; i++) {
                TreeNode head = queue.poll();
                level.add(head.val);
                if (head.left != null)
                    queue.offer(head.left);
                if (head.right != null)
                    queue.offer(head.right);
            }
            result.add(level); // important
        }
        
        return result;
    }

## Question list

__BFS__

1. __[Binary Tree Level Order Traversal]({% post_url /leetcode/2014-05-25-Binary-Tree-Level-Order-Traversal %})__

1. __[Binary Tree Level Order Traversal II]({% post_url /leetcode/2014-05-25-Binary-Tree-Level-Order-Traversal-II %})__

1. __[Binary Tree Zigzag Level Order Traversal]({% post_url /leetcode/2014-05-25-Binary-Tree-Zigzag-Level-Order-Traversal %})__

__Additional__

1. __[Construct Binary Tree from Preorder and Inorder]({% post_url /leetcode/2014-05-27-Construct-Binary-Tree-from-Preorder-and-Inorder %})__

1. __[Construct Binary Tree from Inorder and Postorder]({% post_url /leetcode/2014-05-27-Construct-Binary-Tree-from-Inorder-and-Postorder %})__

## Code

First 3 questions are basically same. Below code is for question 1. There is no 'catch-ya', it's very standard code. 

    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> ans = new LinkedList<List<Integer>>();
		if (root == null) {
			return ans;
		}
		Queue<TreeNode> q = new LinkedList<TreeNode>();
		q.offer(root);
		while(!q.isEmpty()) {
			int size = q.size();
			List<Integer> level = new LinkedList<Integer>();
			for (int i = 0; i < size; i ++) {
				TreeNode node = q.poll();
				level.add(node.val);
				if (node.left != null) {
					q.offer(node.left);
				}
				if (node.right != null) {
					q.offer(node.right);
				}
			}
			ans.add(level);
		}
		return ans;
    }

__Construct Binary Tree from Preorder and Inorder__ - written by me

    public TreeNode buildTree(int[] preorder, int[] inorder) {
		if (preorder == null || inorder == null || preorder.length != inorder.length) {
			return null;
		}
        return helper(preorder, 0, preorder.length-1, inorder, 0, inorder.length-1);
    }
	
	private TreeNode helper(int[] preorder, int a, int b, int[] inorder, int c, int d) {
		if (a > b) {
			return null;
		}
		int headVal = preorder[a];
		TreeNode head = new TreeNode(headVal);
		int p = c;
		while (p <= d) {
			if (inorder[p] == headVal) {
				break;
			}
			p ++;
		}
		head.left = helper(preorder, a+1, a+p-c, inorder, c, p-1);
		head.right = helper(preorder, b-d+p+1, b, inorder, p+1, d);
		return head;
	}

__Construct Binary Tree from Inorder and Postorder__ - similar to previous code, copied from [ninechap](http://answer.ninechapter.com/solutions/construct-binary-tree-from-inorder-and-postorder-traversal/)

    private int findPosition(int[] arr, int start, int end, int key) {
        int i;
        for (i = start; i <= end; i++) {
            if (arr[i] == key) {
                return i;
            }
        }
        return -1;
    }

    private TreeNode myBuildTree(int[] inorder, int instart, int inend,
            int[] postorder, int poststart, int postend) {
        if (instart > inend) {
            return null;
        }

        TreeNode root = new TreeNode(postorder[postend]);
        int position = findPosition(inorder, instart, inend, postorder[postend]);

        root.left = myBuildTree(inorder, instart, position - 1,
                postorder, poststart, poststart + position - instart - 1);
        root.right = myBuildTree(inorder, position + 1, inend,
                postorder, poststart + position - instart, postend - 1);
        return root;
    }

    public TreeNode buildTree(int[] inorder, int[] postorder) {
        if (inorder.length != postorder.length) {
            return null;
        }
        return myBuildTree(inorder, 0, inorder.length - 1, postorder, 0, postorder.length - 1);
    }

