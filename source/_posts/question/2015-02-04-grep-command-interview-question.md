---
layout: post
title: "[Amazon] Grep command interview question "
comments: true
category: Question

---

### Question 

[link](http://www.careercup.com/question?id=1799)

> You have 50,000 html files, some of which contain phone numbers. How would you create a list of all the files which contain phone numbers? 

### Solution

This is a famous inteview question by former Amazon engineer [Steve Yegge](https://sites.google.com/site/steveyegge2/five-essential-phone-screen-questions): 

> About 25% to 35% of all software development engineer candidates, independent of experience level, cannot solve this problem, even given the entire interview hour and lots of hints. 

This question tests your understanding of scripting languages. 

### Code

    grep -l -R --perl-regexp "\b(\(\d{3}\)\s*|\d{3}-)\d{3}-\d{4}\b" * > output.txt
