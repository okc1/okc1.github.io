---
layout: post
title: "[Google] BST find ceiling "
comments: true
category: q-google

---

### Question 

[link](http://www.careercup.com/question?id=20229674)

> A binary search tree is given. Find the ceiling of given key. Eg. 

                        8
                   3          12
               2      6    10    15
                    4

> Ceiling is [defined](http://www.geeksforgeeks.org/floor-and-ceil-from-a-bst/) as:

> Ceil Value Node: Node with smallest data larger than the key value.

> Testing: 

    key - 13 => 15 
    key - 4 =>6 
    key - 8 =>10

### Solution 

__A really interesting idea__ is to go top-to-bottom, and update value in every __left turn only__. Suggested by the [top answer](http://www.careercup.com/question?id=20229674). 

It's a very very tricky solution. I've never seen this b4. 

### Code

Not my code. 

	public int findCeil(TreeNode node, int num, int found) {
		if (node != null) {
			if (num >= node.val)
				return findCeil(node.right, num, found);
			else
				return findCeil(node.left, num, node.val);
		} else
			return found;
	}

Now input: 

> TreeNode tree = Common.constructBstFromPreorder(new int[] { 40, 20, 10, 30, 60, 50, 70 });

Output: 

    The ceiling of 0 is  10
    The ceiling of 1 is  10
    The ceiling of 2 is  10
    The ceiling of 3 is  10
    The ceiling of 4 is  10
    The ceiling of 5 is  10
    The ceiling of 6 is  10
    The ceiling of 7 is  10
    The ceiling of 8 is  10
    The ceiling of 9 is  10
    The ceiling of 10 is  20
    The ceiling of 11 is  20
    The ceiling of 12 is  20
    The ceiling of 13 is  20
    The ceiling of 14 is  20
    The ceiling of 15 is  20
    The ceiling of 16 is  20
    The ceiling of 17 is  20
    The ceiling of 18 is  20
    The ceiling of 19 is  20
    The ceiling of 20 is  30
    The ceiling of 21 is  30
    The ceiling of 22 is  30
    The ceiling of 23 is  30
    The ceiling of 24 is  30
    The ceiling of 25 is  30
    The ceiling of 26 is  30
    The ceiling of 27 is  30
    The ceiling of 28 is  30
    The ceiling of 29 is  30
    The ceiling of 30 is  40
    The ceiling of 31 is  40
    The ceiling of 32 is  40
    The ceiling of 33 is  40
    The ceiling of 34 is  40
    The ceiling of 35 is  40
    The ceiling of 36 is  40
    The ceiling of 37 is  40
    The ceiling of 38 is  40
    The ceiling of 39 is  40
    The ceiling of 40 is  50
    The ceiling of 41 is  50
    The ceiling of 42 is  50
    The ceiling of 43 is  50
    The ceiling of 44 is  50
    The ceiling of 45 is  50
    The ceiling of 46 is  50
    The ceiling of 47 is  50
    The ceiling of 48 is  50
    The ceiling of 49 is  50
    The ceiling of 50 is  60
    The ceiling of 51 is  60
    The ceiling of 52 is  60
    The ceiling of 53 is  60
    The ceiling of 54 is  60
    The ceiling of 55 is  60
    The ceiling of 56 is  60
    The ceiling of 57 is  60
    The ceiling of 58 is  60
    The ceiling of 59 is  60
    The ceiling of 60 is  70
    The ceiling of 61 is  70
    The ceiling of 62 is  70
    The ceiling of 63 is  70
    The ceiling of 64 is  70
    The ceiling of 65 is  70
    The ceiling of 66 is  70
    The ceiling of 67 is  70
    The ceiling of 68 is  70
    The ceiling of 69 is  70
    The ceiling of 70 is  2147483647
    The ceiling of 71 is  2147483647
    The ceiling of 72 is  2147483647
    The ceiling of 73 is  2147483647
    The ceiling of 74 is  2147483647
    The ceiling of 75 is  2147483647
    The ceiling of 76 is  2147483647
    The ceiling of 77 is  2147483647
    The ceiling of 78 is  2147483647
    The ceiling of 79 is  2147483647
    The ceiling of 80 is  2147483647
    The ceiling of 81 is  2147483647
    The ceiling of 82 is  2147483647
    The ceiling of 83 is  2147483647
    The ceiling of 84 is  2147483647
    The ceiling of 85 is  2147483647
    The ceiling of 86 is  2147483647
    The ceiling of 87 is  2147483647
    The ceiling of 88 is  2147483647
    The ceiling of 89 is  2147483647
    The ceiling of 90 is  2147483647
    The ceiling of 91 is  2147483647
    The ceiling of 92 is  2147483647
    The ceiling of 93 is  2147483647
    The ceiling of 94 is  2147483647
    The ceiling of 95 is  2147483647
    The ceiling of 96 is  2147483647
    The ceiling of 97 is  2147483647
    The ceiling of 98 is  2147483647
    The ceiling of 99 is  2147483647
