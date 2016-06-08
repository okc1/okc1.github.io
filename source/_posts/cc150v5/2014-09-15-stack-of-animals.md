---
layout: post
title: "[CC150v5] 3.7 Stack of Animals "
comments: true
category: CC150v5

---

### Question

> An animal shelter holds only dogs and cats. People must adopt either the "oldest" animals, or they can select whether they would prefer a dog or a cat (and will receive the oldest animal of that type). They cannot select which specific animal they would like. 

> Create the data structures to maintain this system and implement operations such as enqueue, dequeueAny, dequeueDog and dequeueCat. You may use the built-in LinkedList data structure. 

### Solution

There are 2 solutions.

__First one is using a single queue__. This makes 'dequeueAny' easy, but 'dequeueCat' and 'dequeueDog' difficult. 

__Second approach would be using 2 queues for dogs and cats__. We need something like timestamp to be stored (more space usage). 

When we return, we peek both queues are choose the older one. __This is recommended solution in the book__. 

### Code

__from the book__

Animal.java

	public abstract class Animal {
		int order;
		String name;

		public Animal(String n) {
			name = n;
		}

		public abstract String name();

		public boolean isOlderThan(Animal a) {
			return this.order < a.order;
		}
	}

	class Cat extends Animal {
		public Cat(String n) {
			super(n);
		}

		public String name() {
			return "Cat: " + name;
		}
	}

	class Dog extends Animal {
		public Dog(String n) {
			super(n);
		}

		public String name() {
			return "Dog: " + name;
		}
	}

AnimalQueue.java

	public class AnimalQueue {
		LinkedList<Dog> dogs = new LinkedList<Dog>();
		LinkedList<Cat> cats = new LinkedList<Cat>();
		private int order = 0;

		public void enqueue(Animal a) {
			a.order = order;
			order++;
			if (a instanceof Dog) {
				dogs.addLast((Dog) a);
			} else if (a instanceof Cat) {
				cats.addLast((Cat) a);
			}
		}

		public Animal dequeueAny() {
			if (dogs.size() == 0) {
				return dequeueCats();
			} else if (cats.size() == 0) {
				return dequeueDogs();
			}
			Dog dog = dogs.peek();
			Cat cat = cats.peek();
			if (dog.isOlderThan(cat)) {
				return dogs.poll();
			} else {
				return cats.poll();
			}
		}

		public Animal peek() {
			if (dogs.size() == 0) {
				return cats.peek();
			} else if (cats.size() == 0) {
				return dogs.peek();
			}
			Dog dog = dogs.peek();
			Cat cat = cats.peek();
			if (dog.isOlderThan(cat)) {
				return dog;
			} else {
				return cat;
			}
		}

		public int size() {
			return dogs.size() + cats.size();
		}

		public Dog dequeueDogs() {
			return dogs.poll();
		}

		public Dog peekDogs() {
			return dogs.peek();
		}

		public Cat dequeueCats() {
			return cats.poll();
		}

		public Cat peekCats() {
			return cats.peek();
		}
	}
