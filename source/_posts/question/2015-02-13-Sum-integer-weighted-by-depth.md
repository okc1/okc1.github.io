---
layout: post
title: "[LinkedIn] Sum of integer weighted by depth "
comments: true
category: Question

---

### Question 

[link](http://www.careercup.com/question?id=5139875124740096)

    /** 
    * Given a nested list of integers, returns the sum of all integers in the list weighted by their depth 
    * For example, given the list {(1,1),2,(1,10)} the function should return 10 (four 1's at depth 2, one 2 at depth 1) 
    * Given the list {1,{4,{6}}} the function should return 27 (one 1 at depth 1, one 4 at depth 2, and one 6 at depth 3) 
    */ 
    public int depthSum (List<NestedInteger> input) 
    { // ur implementation here} 


    ** 
    * This is the interface that represents nested lists. 
    * You should not implement it, or speculate about its implementation. 
    */ 
    public interface NestedInteger 
    { 
    /** @return true if this NestedInteger holds a single integer, rather than a nested list */ 
    boolean isInteger(); 

    /** @return the single integer that this NestedInteger holds, if it holds a single integer 
    * Return null if this NestedInteger holds a nested list */ 
    Integer getInteger(); 

    /** @return the nested list that this NestedInteger holds, if it holds a nested list 
    * Return null if this NestedInteger holds a single integer */ 
    List<NestedInteger> getList(); 
    }

### Solution

DFS recurse. 

### Code

The algo:

	public int depthSum(List<NestedInteger> input, int weight) {
		// ur implementation here
		int sum = 0;
		for (NestedInteger ni : input) {
			if (ni.isInteger()) {
				sum += ni.getInteger() * weight;
			} else {
				sum += depthSum(ni.getList(), weight + 1);
			}
		}
		return sum;
	}

Interface and Impl:

    /*
     * This is the interface that represents nested lists. You should not implement
     * it, or speculate about its implementation.
     */
    interface NestedInteger {
        /**
         * @return true if this NestedInteger holds a single integer, rather than a
         *         nested list
         */
        boolean isInteger();

        /**
         * @return the single integer that this NestedInteger holds, if it holds a
         *         single integer Return null if this NestedInteger holds a nested
         *         list
         */
        Integer getInteger();

        /**
         * @return the nested list that this NestedInteger holds, if it holds a
         *         nested list Return null if this NestedInteger holds a single
         *         integer
         */
        List<NestedInteger> getList();
    }

    class NestedIntegerImpl implements NestedInteger {

        int num;
        List<NestedInteger> list = new ArrayList<NestedInteger>();

        public NestedIntegerImpl(int number) {
            num = number;
            list = null;
        }

        public NestedIntegerImpl(List<NestedInteger> inputList) {
            num = -1;
            list = inputList;
        }

        @Override
        public boolean isInteger() {
            return list == null;
        }

        @Override
        public Integer getInteger() {
            if (isInteger()) {
                return num;
            }
            return -1;
        }

        @Override
        public List<NestedInteger> getList() {
            return list;
        }
    }
