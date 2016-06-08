---
layout: post
title: "[LinkedIn] Isomorphic Strings "
comments: true
category: Question

---

### Question 

[link](http://www.careercup.com/question?id=5389627422670848)

> Given two (dictionary) words as Strings, determine if they are isomorphic. 

> Two words are called isomorphic if the letters in one word can be remapped to get the second word. Remapping a letter means replacing all occurrences of it with another letter while the ordering of the letters remains unchanged. No two letters may map to the same letter, but a letter may map to itself. 

> Example: 

    given "foo", "app"; returns true 
    we can map 'f' -> 'a' and 'o' -> 'p' 

    given "bar", "foo"; returns false 
    we can't map both 'a' and 'r' to 'o' 

    given "turtle", "tletur"; returns true 
    we can map 't' -> 't', 'u' -> 'l', 'r' -> 'e', 'l' -> 'u', 'e' -'r' 

    given "ab", "ca"; returns true 
    we can map 'a' -> 'c', 'b'

### Solution

My first thought was: map char to char, then check in the hashmap. However, __this will not work__! 

    input: abc, pzz
    check a -> p
    check b -> z
    check c -> z

Using a hashmap __ does not show us __whether 2 chars match to the same char__. In above example, b and c both match to z. 

__Best Solution__, suggested by [urik](http://www.careercup.com/question?id=5389627422670848): 

> HashMap (char, firstSeenIndice) for each string. The encoding of firstSeenIndices shud match. 
>
> E.g. Foo and app both encode to 011 
>
> Abcd and hole both encode to 0123 

### Code

	public boolean isomorphic(String s, String t) {
		if (s.length() != t.length()) {
			return false;
		}
		return (sequence(s).equals(sequence(t)));
	}

	private String sequence(String s) {
		HashMap<Character, Integer> map = new HashMap<Character, Integer>();
		StringBuilder sb = new StringBuilder();

		for (int i = 0; i < s.length(); i++) {
			if (map.containsKey(s.charAt(i))) {
				sb.append(map.get(s.charAt(i)));
			} else {
				map.put(s.charAt(i), i);
			}
		}
		return sb.toString();
	}
