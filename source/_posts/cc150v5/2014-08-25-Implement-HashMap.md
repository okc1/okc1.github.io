---
layout: post
title: "[CC150v5] 8.10 Implement a Hashmap"
comments: true
category: CC150v5

---

### Question

> Design and implement a hash table which uses chaining (linked lists) to handle collisions.

### Solution

I wrote this topic before (using Java source code as a reference). This time, I would like to take another (easier) approach. 

The main part of this is to use an array of list structure like this: 

	LinkedList<Cell<K, V>>[] items;

And the Cell Class looks like this: 

    public class Cell<K, V> {
        private K key;
        private V value;

        public Cell(K k, V v) {
            key = k;
            value = v;
        }

        public boolean equivalent(Cell<K, V> c) {
            return equivalent(c.getKey());
        }

        public boolean equivalent(K k) {
            return key.equals(k);
        }

        public K getKey() {
            return key;
        }

        public V getValue() {
            return value;
        }
    }

### Code

__written by me__

    public class HashMapCC150<K, V> {

        int size;
        LinkedList<Cell<K, V>>[] items;

        public HashMapCC150(int num) {
            this.size = num;
            items = (LinkedList<Cell<K, V>>[]) new LinkedList[10];
        }

        public V get(K k) {
            int hashValue = this.calculateHashCode(k);
            if (items[hashValue] == null) {
                items[hashValue] = new LinkedList<Cell<K, V>>();
                return null;
            }
            for (Cell<K, V> cell : items[hashValue]) {
                if (k.equals(cell.getKey())) {
                    return cell.getValue();
                }
            }
            return null;
        }

        public V put(K k, V v) {
            int hashValue = this.calculateHashCode(k);
            if (items[hashValue] == null) {
                items[hashValue] = new LinkedList<Cell<K, V>>();
            }
            for (Cell<K, V> cell : items[hashValue]) {
                if (k.equals(cell.getKey())) {
                    items[hashValue].remove(cell);
                    break;
                }
            }
            Cell<K, V> newItem = new Cell<K, V>(k, v);
            items[hashValue].add(newItem);
            return null;
        }

        public V remove(K k) {
            // not written
            return null;
        }

        private int calculateHashCode(K k) {
            return k.toString().length() % size;
        }

        public static void main(String[] args) {
            HashMapCC150<String, String> map = new HashMapCC150<String, String>(10);
            map.put("kevin", "durant");
            map.put("steven", "curry");
            map.put("al", "jefferson");
            System.out.println(map.get("kevin"));
            System.out.println(map.get("steven"));
            System.out.println(map.get("al"));
            map.put("kevin", "martin");
            map.put("steven", "nash");
            map.put("kevin", "braynt");
            System.out.println(map.get("kevin"));
            System.out.println(map.get("steven"));
            System.out.println(map.get("al"));
        }
    }

    class Cell<K, V> {
        private K key;
        private V value;

        public Cell(K k, V v) {
            key = k;
            value = v;
        }

        public boolean equivalent(Cell<K, V> c) {
            return equivalent(c.getKey());
        }

        public boolean equivalent(K k) {
            return key.equals(k);
        }

        public K getKey() {
            return key;
        }

        public V getValue() {
            return value;
        }
    }
