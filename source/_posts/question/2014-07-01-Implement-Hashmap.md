---
layout: post
title: "[Question] Implement a HashMap"
comments: true
category: Question

---


### Question 

Implement a HashMap

__Hint__:

> An instance of HashMap has two parameters that affect its performance: initial capacity and load factor. The capacity is the number of buckets in the hash table, and the initial capacity is simply the capacity at the time the hash table is created. The load factor is a measure of how full the hash table is allowed to get before its capacity is automatically increased. When the number of entries in the hash table exceeds the product of the load factor and the current capacity, the hash table is rehashed (that is, internal data structures are rebuilt) so that the hash table has approximately twice the number of buckets. [source](http://stackoverflow.com/a/10901821)
>
> Load factor = n/k where n is the number of entries and k is the number of buckets. 

### Analysis

Some points to take note: 

1. So first of all, we would need 2 important parameters in a Hashmap: __initial capacity and load factor__. In Java, it's default 0.75. 
    
    For example the product of capacity and load factor = 16 * 0.75 = 12. This represents that after storing the 12th key – value pair into the HashMap , its capacity will become 32.

1. Then we would need an Entry<Obj, Obj> Class to store __key-value pairs__. Important to note the Entry would have a 'next' pointer, in order to mimic a LinkedList. 

1. Except key, value and next pointer, Entry class __also need to store the 'hash' value__, because it will be used during comparison. 

1. The main bucket is an array of Entry objects. It should resize when it has to, and this is __done in the addEntry() method__. I skipped this part of code. 

1. The code for put() and get() method are similar, because it's bascially __calculate hash__, then __get array index__, using that index to __locate the head Entry object__, and then do a linear search for key. If found, put() will replace it, and get() will return it. Note than after replaced, the old value is returned (Java designed in this way, I personally wouldn't do this). 

1. Last important thing is the __indexFor() method__. It looks useless to me at first, then I realize that this method is mapping my hash value into the index in the array. Fine, but this bit operation still looks odd. Look at next section for more. 

### The Niubility Operation: h & (length - 1)

This actually equals to the value of (h % length). It converts the hash value into array index. 

> 这个方法非常巧妙，它通过 h & (length - 1) 来得到该对象的保存位，而HashMap底层数组的长度总是 2 的 n 次方，这是HashMap在速度上的优化。
>
> 当length总是 2 的n次方时，h & (length - 1)运算等价于对length取模，也就是h % length，但是 & 比 % 具有更高的效率。[source](http://www.cnblogs.com/-clq/archive/2012/01/11/2318870.html)

That's all about implementing a HashMap. It's difficult, but having a general idea definitely helps. 

What's more, know the mod operation "h & (length - 1)" would definitely help you grab some attentions! 

### Code

    public class MyHashMap {

        Pair[] table;
        float loadFactor;
        int size;

        public MyHashMap(int initialCapacity, float loadFactor) {
            if (initialCapacity < 0 || loadFactor <= 0) {
                return;
            }
            table = new Pair[initialCapacity];
            this.size = 0;
            this.loadFactor = loadFactor;
        }

        public String get(int key) {
            int hash = hash(key);
            int i = indexFor(hash, table.length);
            Pair e = table[i];
            for (; e != null; e = e.next) {
                if (e.hash == hash && key == e.key) {
                    return e.value;
                }
            }
            return null;
        }

        public String put(int key, String value) {
            int hash = hash(key);
            int i = indexFor(hash, table.length);
            Pair e = table[i];
            for (; e != null; e = e.next) {
                if (e.hash == hash && key == e.key) {
                    String oldValue = e.value;
                    e.value = value;
                    return oldValue;
                }
            }
            addEntry(hash, key, value, i);
            return null;
        }

        void addEntry(int hash, int key, String value, int i) {
            // in charge of resizing here (check the load factor)
            // resizing code is not written here
            Pair e = table[i];
            table[i] = new Pair(hash, key, value, e);
        }

        int indexFor(int h, int length) {
            return h & (length - 1);
        }

        final int hash(int code) {
            // this is the hash function from java 6 source code
            code ^= (code >>> 20) ^ (code >>> 12);
            return code ^ (code >>> 7) ^ (code >>> 4);
        }

        public static void main(String[] args) {
            MyHashMap map = new MyHashMap(16, 0.5f);
            map.put(1, "a");
            map.put(2, "b");
            map.put(3, "c");
            System.out.println(map.get(1));
            System.out.println(map.get(2));
            System.out.println(map.get(3));
            map.put(1, "Spider Man");
            map.put(4, "d");
            map.put(3, "Peter Parker");
            System.out.println(map.get(1));
            System.out.println(map.get(2));
            System.out.println(map.get(3));
            System.out.println(map.get(4));
            System.out.println(map.get(5));
        }

        class Pair {
            int hash;
            int key;
            String value;
            Pair next;

            Pair(int h, int k, String v, Pair n) {
                hash = h;
                key = k;
                value = v;
                next = n;
            }
        }
    }
