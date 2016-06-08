---
layout: post
title: "[LeetCode 187] Repeated DNA Sequences "
comments: true
category: Leetcode
---

### Question

[link](https://leetcode.com/problems/repeated-dna-sequences/)

<div class="question-content">
              <p></p><p>
All DNA is composed of a series of nucleotides abbreviated as A, C, G, and T, for example: "ACGAATTCCG". When studying DNA, it is sometimes useful to identify repeated sequences within the DNA.</p>

<p>Write a function to find all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule.</p>

<p>
For example,</p>
<pre>Given s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT",

Return:
["AAAAACCCCC", "CCCCCAAAAA"].
</pre><p></p>

                <div id="tags" class="btn btn-xs btn-warning">Show Tags</div>
                <span class="hide">

                  <a class="btn btn-xs btn-primary" href="/tag/hash-table/">Hash Table</a>

                  <a class="btn btn-xs btn-primary" href="/tag/bit-manipulation/">Bit Manipulation</a>

                </span>

            </div>

### Analysis

This question is straight-forward: just iterate thru all the 10-letter long subsequences, and then add into hashmap.

However, if you simply use String as hash key, it will exceed OJ run time.

### Solution

Convert string to int is the right approach. To get the best performance, we use 2 bits to represent each DNA nucleotide. Integer is 32-bit long so, no problem with that. 

Node that Integer.Max = 2,147,483,647. There's total of 10 digitals, so using 1 digit to represent 1 letter is not feasible.
Ref: [BUPT-哲人善思](http://www.cnblogs.com/hzhesi/p/4285793.html)

### Code

The code is pretty difficult to write.

    public class Solution {
        public List<String> findRepeatedDnaSequences(String s) {
            List<String> res = new ArrayList<String>();
            if (s == null || s.length() < 10) {
                return res;
            }
            
            Map<Integer, Integer> map = new HashMap<Integer, Integer>();
            // map<> stores int-to-int: first int is "ACGT" -> 1234
            // second int is the init position of the pattern in s
            
            int num = 0;
            int mask = 0xFFFFFFFF;
            mask >>>= (32 - 18);
            
            for (int i = 0; i < s.length(); i++) {
                num = mask & num;
                // get the last 18 binary digits of num
                
                num = (num << 2) | convertChatToInt(s.charAt(i));
                // append num with the number representing charAt(i)
                
                if (i >= 9) {
                    // insert or search num in the map
                    if (!map.containsKey(num)) {
                        map.put(num, (i - 9));
                        // (i - 9) is the start position of 
                        // the 10-letter-long sequence
                    } else if (map.get(num) != -1) {
                        res.add(s.substring(map.get(num), map.get(num) + 10));
                        map.put(num, -1);
                        // after the sequence has been added, mark it in the map
                    } else {
                        // do nothing
                    }
                }
            }
            
            return res;
        }
        
        int convertChatToInt(char ch) {
            if (ch == 'A') {
                return 1;
            } else if (ch == 'C') {
                return 2;
            } else if (ch == 'G') {
                return 3;
            }
            return 0;
        }
    }

