---
layout: post
title: "[Question] Truth tell brain teaser"
comments: true
category: Question

---

### Question 

[link](http://tech-queries.blogspot.sg/2011/07/truth-or-lie.html)

> There are 100 people in a room. A person always speaks either lie or truth. 

> When asked:

    1st person says => all are liars
    2nd person says => at most 1 speaks truth
    3rd person says => at most 2 speak truth
    4th person says => at most 3 speak truth
    .
    .
    .
    100th person says => at most 99 speak truth

> "At most N" means "there're N or less than N". 

> How many people speak only truth?

### Solution

50. 

1. Assume 1st person speaks truth, then all including him should be liar. It means he doesn’t speak truth. 

1. Assume 2nd person speaks truth, then he is the only person who speaks truth. But if this statement is true then statements by all others are also true. I.e. if “at most 1 person speaks truth” is true then “at most N speak truth” is also true. So person 2 is also a liar.

1. Assume 3rd person is speaking truth. But then the statements of person 4-100 are also true, which contradicts his own statement. It means that person 3 is also a liar.

1. This process will continue since 50th person. So 1-50 people are liars.

1. 51st person says “at most 50 speak truth”. Lets say he is speaking truth. “at most 50” means any number from 0-50. It means that statements like “at most 51 speak truth” and “at most 70 speak truth” are also true. It means that people from 51 to 100 are speaking truth.

__Hence, 50 people speak truth__.
