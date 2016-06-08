---
layout: post
title: "[CC150v5] 8.1 Design a Generic Deck of Cards"
comments: true
category: CC150v5

---

### Question 

> Design a Generic Deck of Cards

### Solution

A simple design: 

	enum Suit {
		HEART, DIAMOND, SPADES, CLUBS;
	}

	class Deck {
		List<Card> deck;
	}

	class Card {
		Suit suit;
		int num;
	}

A more complex design: 

	enum Suit {
		HEART, DIAMOND, SPADES, CLUBS;
	}

	class Deck<T extends Card> {
		List<Card> deck;

		public void shuffle() {
		};
	}

	abstract class Card {
		boolean available;
		Suit suit;
		int num;

		public boolean isAvailable() {
			return available;
		};
	}

	class Hand<T extends Card> {
		List<Card> cards;

		public int score() {
			int score = 0;
			for (Card c : cards) {
				score += c.num;
			}
			return score;
		}

		public void addCard(T card) {
			cards.add(card);
		}
	}

	// Now use the above generic Data Structure to make a
	// Blackjack Game
	class Blackjack extends Hand<BlackJackCard> {
	}

	class BlackJackCard extends Card {
	}
