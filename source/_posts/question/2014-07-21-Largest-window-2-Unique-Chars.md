---
layout: post
title: "[Question] Longest Substring with At Most Two Distinct Characters "
comments: true
category: Question
tags: [ src ]
---

### Question

[link](http://www.programcreek.com/2013/02/longest-substring-which-contains-2-unique-characters/)

> Given a string, find the longest substring that contains only two unique characters. For example, given "abcbbbbcccbdddadacb", the longest substring that contains 2 unique character is "bcbbbbcccb".

### Solution

__First, the most basic and naive solution__, which we use 2 pointers and 1 hashset. Read thru and when seeing the 3rd different char, __rebuild the hashset__. Idea is from original post. This approach is not very efficient. 

__Second, we can use HashMap instead of HashSet__, so that we keep couting how many of each char we currently got. This should do the trick well. 

> What if the question change from '2 unique chars' to 'N unique chars'? __Use HashMap instead of HashSet__. The rest of the is very similar. 

__Third solution I found it [here](http://stackoverflow.com/a/15000204)__. It keeps a 'lastGroupStart' pointer, that points to __the last position where character changes__. Eg. "aaaabbbbbcccc", 'lastGroupStart' would pointer to the first occurance of 'b'. When we read until c, we update the window starting point to 'lastGroupStart', and update 'lastGroupStart' to the first occurance of 'c'. 

This is a frequent question. I personally would __recommend 2nd solution: using HashMap__. 

### Code

__first solution__

	private String solution(String input) {
		HashSet<Character> set = new HashSet<Character>();
		char[] letters = input.toCharArray();
		set.add(letters[0]);

		int start = 0;
		String longest = input.substring(0, 1);

		for (int i = 1; i < input.length(); i++) {
			if (set.add(letters[i])) {
				if (set.size() > 2) {
					// first, update the longest substring that exists before i
					if (i - start > longest.length()) {
						longest = input.substring(start, i);
					}
					// clear and rebuild the HashSet
					set.clear();
					set.add(letters[i]);
					set.add(letters[i - 1]);
					// remove 1 char entirely from current substring
					int p = i - 1;
					while (p > 0 && letters[p] == letters[p - 1]) {
						p--;
					}
					start = p;
				}
			}
		}
		if (input.length() - start > longest.length()) {
			longest = input.substring(start);
		}
		return longest;
	}

__third solution__, pay attention to 'lastGroupStart'. 

    // Find the first letter that is not equal to the first one, 
    // or return the entire string if it consists of one type of characters
    int start = 0;
    int i = 1;
    while (i < str.length() && str[i] == str[start])
        i++;
    if (i == str.length())
        return str;

    // The main algorithm
    char[2] chars = {str[start], str[i]};
    int lastGroupStart = 0;
    while (i < str.length()) {
        if (str[i] == chars[0] || str[i] == chars[1]) {
            if (str[i] != str[i - 1])
                lastGroupStart = i;
        }
        else {
            //TODO: str.substring(start, i) is a locally maximal string; 
            //      compare it to the longest one so far
            start = lastGroupStart;
            lastGroupStart = i;
            chars[0] = str[start];
            chars[1] = str[lastGroupStart];
        }
        i++;
    }
    //TODO: After the loop, str.substring(start, str.length()) 
    //      is also a potential solution.
