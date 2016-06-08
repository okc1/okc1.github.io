---
layout: post
title: "[Question] Which loop is faster"
comments: true
category: Question

---

### Question 

[link](http://tech-queries.blogspot.sg/2010/09/which-loop-is-faster.html)

> A very basic programming puzzle is being asked in programming interviews since last few years. Which of the below two loops will run faster? 

	/* First */  
	for(i=0;i<100;i++)  
	 for(j=0;j<10;j++)  
	     //do somthing

	/* Second */  
	for(i=0;i<10;i++)  
	 for(j=0;j<100;j++)  
	     //do somthing  

### Solution

1. The First executes assignment operations 101 times, while Second executes only 11 times.
1. The First does 101 + 1100 = 1201 comparisons, while the Second does 11 + 1010 = 1021 comparisons. 
1. The First executes 1100 increments, while the Second executes 1010 increments. 

### Code

The following code proves why First is faster. 

	public static void solution() {
		int i, j, k, l;
		k = 0;
		l = 0;
		/* FIRST */
		for (i = 0, l++; i < 10; i++, k++)
			for (j = 0, l++; j < 100; j++, k++)
				;
		// printf("First Loop: %d\t%d\n", k, l);
		System.out.println(k);
		System.out.println(l);

		k = 0;
		l = 0;
		/* SECOND */
		for (i = 0, l++; i < 100; i++, k++)
			for (j = 0, l++; j < 10; j++, k++)
				;
		// printf("Second Loop: %d\t%d\n", k, l);
		System.out.println(k);
		System.out.println(l);
	}

output is : 1010, 11, 1100, 101
