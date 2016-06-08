---
layout: post
title: "[Question] First Character Appearing Only Once"
comments: true
category: Question
tags: [ unit test needed ]
---


### Question 

[link](http://codercareer.blogspot.sg/2011/10/no-13-first-character-appearing-only.html)

> Problem: Implement a function to find the first character in a string which only appears once.
    For example: It returns ‘b’ when the input is “abaccdeff”.

### Analysis 

Great solution from [Ryan](http://stackoverflow.com/a/2285561): 

> You can't know that the character is un-repeated until you've processed the whole string, so my suggestion would be...

Keep 2 lists. 

One stores chars that appear once, the other list stores repeated chars. 

Code is shown below. 

    def first_non_repeated_character(string):
      chars = []
      repeated = []
      for character in string:
        if character in chars:
          chars.remove(character)
          repeated.append(character)
        else:
          if not character in repeated:
            chars.append(character)
      if len(chars):
        return chars[0]
      else:
        return False