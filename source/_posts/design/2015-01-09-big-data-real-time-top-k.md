---
layout: post
title: "[Design] Real Time Top k "
comments: true
categories:
- Design
- z-top-K

---

### Question 

[link](http://stackoverflow.com/questions/10189685/realtime-tracking-of-top-100-twitter-words-per-min-hour-day)

> Given a continuous twitter feed, design an algorithm to return the 100 most
frequent words used at this minute, this hour and this day. 

### Analysis

This is a frequent and useful problem for companies like Google and Twitter. 

The first solution below is __an approximation method__ which select keywords that occur more than a certain threshold. 

The second solution is __more accurate__ but RAM-intensive. 

### Lossy Count (used to get an inaccurate trend) 

__Solution 1 is a modified version of [Lossy Count](http://stackoverflow.com/a/8033083)__. The detailed steps are explained [here](http://stackoverflow.com/a/3260905): 

> Start with an empty map (red-black tree). The keys will be search terms, and the values will be a counter for the term. 
>
> 1. Look at each item in the stream.
>
> 1. If the term exists in the map, increment the associated counter.
>
> 1. Otherwise, if the map has fewer candidates than you're looking for, add it to the map with a count of one.
>
> 1. However, if the map is "full", decrement the counter in each entry. If any counter reaches zero during this process, remove it from the map.

[This slide show](http://www.cse.ust.hk/vldb2002/VLDB2002-proceedings/slides/S10P03slides.pdf) explains __Lossy Count__, which is to divide input data into chunks. Then count elements and decrease counter by 1 after each chunk. 

__Note that the result is NOT the top frequency items__. Instead, the final results are __order-dependent__, giving heavier weight to the counts processed last. It maybe helpful in some cases, cuz we want to check the latest trend. However, if we want more accurate top keywords for all data, we will __do a second pass over the log data__. 

Now let's discuss the threshold. Use "aaabcd" and map size = 2 as example. 'a' will be inserted into map with occurance = 3. Then 'b' is inserted, and removed. 'c' is inserted, and removed. 'd' is inserted. Since we always decrease 1 at each step, 'a' should only have occurance of 1 at the end. As explained [here](http://stackoverflow.com/a/3260905): 

> If we limit the map to 99 entries, we are guaranteed to find any term that occurs more than 1/(1 + 99) (1%) of the time. 

We change the size of the map to change the threshold. The occurance of in the final result does not matter. 

### Solution 2

The lossy count does not actually produce the hourly, daily and monthly result accurately. Solution 2 will discuss how we deal with retiring old data in an accurate way. 

Suggested by [this answer](http://stackoverflow.com/a/3260768), __we keep a 30-day list for each keyword__, that counts the daily occurance. This list is FIFO. When we remove and insert a new counter value, we update monthly total. 

Alaternatively, [this answer](http://stackoverflow.com/a/10190836) suggests keeping 1440 (24 * 60) HashMaps, each storing the information for one minute. __And another 2 HashMap for the rolling total for the past hour, and past day__. 

> You need an array of 1440 (24*60) word+count hash maps organized the way that you describe; these are your minute-by-minute counts. You need two additional hash maps - for the rolling total of the hour and the day.

> Define two operations on hash maps - add and subtract, with the semantic of merging counts of identical words, and removing words when their count drops to zero.

> Each minute you start a new hash map, and update counts from the feed. At the end of the minute, you place that hash map into the array for the current minute, add it to the rolling total for the hour and for the day, and then subtract the hash map of an hour ago from the hourly running total, and subtract the hash map of 24 hours ago from the daily running total.

This is a very good solution, which I would recommend as the standard solution to this "Real Time Top k" problem. 
