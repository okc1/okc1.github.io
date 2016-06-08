---
layout: post
title: "[Google] Find Anagrams in Dictionary "
comments: true
category: q-google

---

### Question 

[link](http://www.careercup.com/question?id=3088)

> Imagine you had a dictionary. How would you print all anagrams of a word? What if you had to do this repeatedly? Could you optimize it?

### Solution

A very [nice solution](http://stackoverflow.com/a/12477976): 

1. Open dictionary

1. Create empty hashmap H

1. For each word in dictionary:

    1. Create a key that is the word's letters sorted alphabetically (and forced to one case)
    
    1. Add the word to the list of words accessed by the hash key in H

There's another [very interesting idea](http://karmaandcoding.blogspot.sg/2012/02/print-all-anagrams-for-word-from.html), if the length of the word is not too long. 

> Another approach could be we can assign each letters from a..z a prime numbers (2, 3, 5, 7, 11, 13, 17, 19, 23, 29, .. so on)
>
> and then for any word, we can calculate its key as the multiples of all the prime number corresponding to characters in the word. 
>
> The char -> int assignment may look like: 

    a=2, b=3, c=5, d=7, e=11, f=13, g=17, h=19, i=23, j=29, 
    k=31, l=37, m=41, n=43, o=47, p=53, q=59, r=61, s=67, t=71, 
    u=73, v=79, w=83, x=89, y=97, z=101

### Code

__not written by me__, [link](http://karmaandcoding.blogspot.sg/2012/02/print-all-anagrams-for-word-from.html)

	private static HashMap<String, ArrayList<String>> anagramMap = new HashMap<String, ArrayList<String>>();

	public static void findAnagrams(String[] dictionary) {
		int len = dictionary.length;

		for (int i = 0; i < len; i++) {
			String sortedWord = sortWordLexicographically(dictionary[i]);
			ArrayList<String> wordList = anagramMap.get(sortedWord);
			if (wordList == null) {
				wordList = new ArrayList<String>();
			}
			wordList.add(dictionary[i]);
			anagramMap.put(sortedWord, wordList);
		}
	}

	public ArrayList<String> getAnagrams(String word) {
		if (word == null) {
			return null;
		}

		String sortedWord = sortWordLexicographically(word);
		return anagramMap.get(sortedWord);
	}

	public void printAnagrams(String word) {
		if (word == null) {
			System.out.println("Input word is null!");
		} else {
			ArrayList<String> wordList = getAnagrams(word);
			if (wordList == null) {
				System.out.println("No anagrams exists for : " + word);
			} else {
				Iterator<String> iter = wordList.iterator();
				while (iter.hasNext()) {
					System.out.print(iter.next());
				}
			}
		}
	}
