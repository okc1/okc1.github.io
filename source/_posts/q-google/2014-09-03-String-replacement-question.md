---
layout: post
title: "[Google] String Replacement Question "
comments: true
category: q-google

---

### Question 

[link](http://www.mitbbs.com/article_t/JobHunting/32766461.html)

> String replace, 给一个原string，一个target，一个替换的新str，把所有出现
target str的地方都换成新的str， 长度可以任意. 

### Solution

If the question asks for an in-place algo, then we can refer to __Question 1.5 in CC150v4__. 

### Question 

> 1.5 Write a method to replace all spaces in a string with ‘%20’. 

### Solution

1. __pre-processing__, count the number of spaces in string
2. parse the string from end to beginning. 

Need 2 pass.

### Code

__not written by me__

	public static void ReplaceFun(char[] str, int length) {
		int spaceCount = 0, newLength, i = 0;
		for (i = 0; i < length; i++) {
			if (str[i] == ' ') {
				spaceCount++;
			}
		}
		newLength = length + spaceCount * 2;
		str[newLength] = '\0';
		for (i = length - 1; i >= 0; i--) {
			if (str[i] == ' ') {
				str[newLength - 1] = '0';
				str[newLength - 2] = '2';
				str[newLength - 3] = '%';
				newLength = newLength - 3;
			} else {
				str[newLength - 1] = str[i];
				newLength = newLength - 1;
			}
		}
	}
