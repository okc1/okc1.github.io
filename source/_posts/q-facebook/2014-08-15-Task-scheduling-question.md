---
layout: post
title: "[Facebook] Task Scheduling Question "
comments: true
category: q-facebook
tags: [ src ]
---

### Question 

[link](http://www.itint5.com/oj/#10)

> 有n个任务需要完成（编号1到n），任务之间有一些依赖关系，如果任务a依赖于任务b和c，那么只有当任务b和任务c完成之后才能完成任务a。给定所有的依赖关系，判断这些任务是否能够完成。如果能够完成，请给出一个合法的任务完成序列。

> 样例：
>
>n=5
>
>1->2,3
>
>3->4
>
>上述样例中任务1依赖于任务2和任务3，任务3依赖于任务4，那么存在合法的任务完成序列4,3,2,1,5

### Solution

__Classic topology sorting__, refer to [this nice answer](http://www.itint5.com/discuss/8/%E4%BB%BB%E5%8A%A1%E8%B0%83%E5%BA%A6java%E7%A8%8B%E5%BA%8F). 

### My Code

	public int[] myJobSchedulerWithoutQueue(Map<Integer, List<Integer>> deps,
			int n) {
		int[] ans = new int[n];

		int[] depCount = new int[n];
		// eg. job 1 depends on job 2 and 3, thus depCount[1-1] = 2
		Map<Integer, List<Integer>> graph = new HashMap<Integer, List<Integer>>();
		// graph would be reversed version of deps, used for topology sorting
		// eg. 2 would point to 1, and 3 would points to 1
		for (int i : deps.keySet()) {
			depCount[i - 1] = deps.get(i).size();
			for (int j : deps.get(i)) {
				// add (j, i) pair into graph
				if (!graph.containsKey(j)) {
					graph.put(j, new ArrayList<Integer>());
				}
				graph.get(j).add(i);
			}
		}
		// now we got depCount[] and graph ready, let's rock
		int sorted = 0;
		while (sorted != n) {
			// first find a 'p' so that depCount[p] = 0
			int p = 0;
			while (p < n && depCount[p] != 0) {
				p++;
			}
			if (p == n) {
				// unable to find a new node to sort, sorting failed
				break;
			}
			// remember p is only the index, the value should be +1
			int val = p + 1;
			ans[sorted++] = val;
			depCount[p] = -1;
			if (graph.containsKey(val)) {
				for (int i : graph.get(val)) {
					depCount[i - 1]--;
				}
			}
		}
		if (sorted == n)
			return ans; // sort sucess
		else
			return null; // sort failed
	}

The following is very similar implementation, but using a Queue to store temporary nodes. 

	public int[] myJobSchedulerWithQueue(Map<Integer, List<Integer>> deps, int n) {
		int[] ans = new int[n];

		int[] depCount = new int[n];
		// eg. job 1 depends on job 2 and 3, thus depCount[1-1] = 2
		Map<Integer, List<Integer>> graph = new HashMap<Integer, List<Integer>>();
		// graph would be reversed version of deps, used for topology sorting
		// eg. 2 would point to 1, and 3 would points to 1
		for (int i : deps.keySet()) {
			depCount[i - 1] = deps.get(i).size();
			for (int j : deps.get(i)) {
				// add (j, i) pair into graph
				if (!graph.containsKey(j)) {
					graph.put(j, new ArrayList<Integer>());
				}
				graph.get(j).add(i);
			}
		}
		// now we got depCount[] and graph ready, let's rock
		int sorted = 0;
		Queue<Integer> queue = new LinkedList<Integer>();
		while (sorted != n) {
			for (int i = 0; i < depCount.length; i++) {
				if (depCount[i] == 0) {
					queue.offer(i + 1);
					depCount[i] = -1;
				}
			}
			if (queue.isEmpty()) {
				break; // sorting failed
			}
			int val = queue.poll();
			ans[sorted++] = val;
			if (graph.containsKey(val)) {
				for (int i : graph.get(val)) {
					depCount[i - 1]--;
				}
			}
		}
		if (sorted == n)
			return ans; // sort sucess
		else
			return null; // sort failed
	}
