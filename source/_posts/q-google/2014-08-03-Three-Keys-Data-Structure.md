---
layout: post
title: "[Google] Three Keys Data Structure"
comments: true
category: q-google

---

### Question 

[link](http://www.careercup.com/question?id=5763793837621248)

> Give efficient implementation of the following problem. 

> An item consist of different keys say k1, k2, k3. User can insert any number of items in database, search for item using __any (one) key__, delete it using any key and iterate through all the items in sorted order __using any key__. Give the most efficient way such that it supports insertion, search based on a key, iteration and deletion.

### Solution

There're 3 keys, so we need 3 maps to store search map for 3 types of keys. For example, the DS is like this: 

> (date, name, country) -> ItemObject

Then we would have: 

> date -> a list of ItemObject
>
> name -> a list of ItemObject
>
> country -> a list of ItemObject

Since we need to iterate in order, we choose TreeMap over HashMap. 

For scalability purpose, we use another HashMap<KeyType, TreeMap> and put 3 items in. 

### Final Data Structure

3 DS needed. [source](http://www.careercup.com/question?id=5763793837621248)

1. ArrayList<ItemObject> list;
1. TreeMap<KeyValue, List<ItemObject>> index; 
1. HashMap<KeyType, TreeMap<KeyValue, List<ItemObject>>> mapOfIndexes;

#### Method add(item): void 

1. add item in ArrayList. 
1. For each key, get TreeMap from HashMap and add into TreeMap. 

#### Method search(key): List<Item> 

1. Get TreeMap from HashMap for provided key.
1. Search the TreeMap
1. Return List Of Items 

#### Method delete(key): List<Item> 

1. Using search method get List Of item 
2. Delete items from ArrayList and __also delete its mapping from all (3) TreeMap__

#### Method orderedIterator(keytype): Iterator 

1. Get TreeMap from HashMap for provided key 
2. Get EntrySet from TreeMap 
3. Return EntrySet.iterator(); 
