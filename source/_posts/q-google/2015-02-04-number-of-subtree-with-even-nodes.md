---
layout: post
title: "[Google] Number of subtrees with even nodes "
comments: true
category: q-google

---

### Question 

[link](http://www.mitbbs.com/article_t0/JobHunting/32348573.html)

> an arbitrary tree. split it into as many subtrees as you can. the 
number of nodes of the subtree must be even.

### Solution

__This is a difficult question__. The idea is recursive solution, but be cautious deadling with NULL. 

__NULL can be regarded as a child branch of even node (0)__, but NULL could not be seen as a subtreee. 

1. traverse each and every node in the tree
1. for each node, take it as root, and find left and right branch with total sum of odd count of nodes. 
1. we do above step recursively
1. include NULL as a subtree of EVEN number of nodes. 

The code below is my code and I haven't seen any reference to this question. If you read this, please comment and discuss with me! 

### Code

	public void traverseAndFindEvenSubstrees(List<TreeNode> ans, TreeNode node) {
		if (node == null) {
			return;
		}
		List<TreeNode> evenSubtrees = this.getSubtrees(node, true);
		evenSubtrees.remove(null);
		ans.addAll(evenSubtrees);

		traverseAndFindEvenSubstrees(ans, node.left);
		traverseAndFindEvenSubstrees(ans, node.right);
	}

	private List<TreeNode> getSubtrees(TreeNode root, boolean isEven) {
		List<TreeNode> ans = new ArrayList<TreeNode>();
		if (root == null) {
			if (isEven) {
				// NULL is considered as a subtree with even number (0) of nodes
				ans.add(null);
			}
			return ans;
		}
		if (isEven) {
			// we need 2 subtrees to have a combined nodes of odd numbers
			for (int i = 0; i <= 1; i++) {
				List<TreeNode> leftGroup = getSubtrees(root.left, i == 0);
				List<TreeNode> rightGroup = getSubtrees(root.right, i != 0);
				// what we do here, is to make leftGroup and rightGroup have
				// different boolean parameter, thus a total of odd count
				for (TreeNode ln : leftGroup) {
					for (TreeNode rn : rightGroup) {
						// note that NULL is included in either leftGroup or
						// rightGroup. we'll use that
						TreeNode newSubtree = new TreeNode(root.val);
						newSubtree.left = ln;
						newSubtree.right = rn;
						ans.add(newSubtree);
					}
				}
			}
			// now we've added all subtrees into ans, whose head is the root
			// this means we does not inlcude NULL
		} else {
			for (int i = 0; i <= 1; i++) {
				List<TreeNode> leftGroup = getSubtrees(root.left, i == 0);
				List<TreeNode> rightGroup = getSubtrees(root.right, i == 0);
				for (TreeNode ln : leftGroup) {
					for (TreeNode rn : rightGroup) {
						TreeNode newSubtree = new TreeNode(root.val);
						newSubtree.left = ln;
						newSubtree.right = rn;
						ans.add(newSubtree);
					}
				}
			}
		}
		// now last step, add NULL (important)
		if (isEven) {
			ans.add(null);
		}
		return ans;
	}

Test data:

    Test start
    Input is a BST with this structure: 
    4 
    2 6 
    1 3 5 7 

    Total subtree count = 16
    They are: 
    Tree 1:
    4 
    2 6 
    3 
    Tree 2:
    4 
    2 6 
    3 5 7 
    Tree 3:
    4 
    2 6 
    1 
    Tree 4:
    4 
    2 6 
    1 5 7 
    Tree 5:
    4 
    6 
    Tree 6:
    4 
    6 
    5 7 
    Tree 7:
    4 
    2 6 
    7 
    Tree 8:
    4 
    2 6 
    5 
    Tree 9:
    4 
    2 
    Tree 10:
    4 
    2 6 
    1 3 7 
    Tree 11:
    4 
    2 6 
    1 3 5 
    Tree 12:
    4 
    2 
    1 3 
    Tree 13:
    2 
    3 
    Tree 14:
    2 
    1 
    Tree 15:
    6 
    7 
    Tree 16:
    6 
    5 
    Total time = 0.006
