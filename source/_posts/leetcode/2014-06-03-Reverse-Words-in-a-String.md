---
layout: post
title: "[LeetCode 151] Reverse Words in a String"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/reverse-words-in-a-string/)

<div class="question-content bg-color bg-img font-color">
<p class="font-color"></p><p class="font-color">
Given an input string, reverse the string word by word.
</p>

<p class="font-color">
For example,<br>
Given s = "<code>the sky is blue</code>",<br>
return "<code>blue is sky the</code>".
</p>

<div>
<b>Clarification:</b>

<p class="font-color">
</p><ul class="bg-color bg-img font-color">
<li>What constitutes a word?<br>
A sequence of non-space characters constitutes a word.</li>
<li>Could the input string contain leading or trailing spaces?<br>
Yes. However, your reversed string should not contain leading or trailing spaces.</li>
<li>How about multiple spaces between two words?<br>
Reduce them to a single space in the reversed string.</li>
</ul>
<p class="font-color"></p>
</div><p class="font-color"></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="yellow">--------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is an very classic question__, and there is a very nice solution. 

### Solution

__First solution is read each character from the back, and insert each word into answer String__. I used this method, and passed in 2 attempts. I have always been afriad of string question, and this time it gave me an easy time. 

I post my code below. Altough it can be better if I use StringBuilder. Most blog/forum would give this solution including [this one](https://oj.leetcode.com/discuss/3378/is-my-solution-good-enough). 

However, previous solution uses extra space. __We can do it in-place suggested by [this post](http://stackoverflow.com/a/1009174)__. 

<blockquote cite="http://stackoverflow.com/a/1009174">
    <p class="font-color">Reverse the entire string, then reverse the letters of each individual word.</p>

    <p class="font-color">After the first pass the string will be</p>

    <pre><code>s1 = "Z Y X si eman yM"
    </code></pre>

    <p class="font-color">and after the second pass it will be</p>

    <pre><code>s1 = "Z Y X is name My"
    </code></pre>
</blockquote>

There are 2 things to note. 

__One, the edge cases__ are easily omitted, like all-space input, double-space in between, and a lot more. 

__Two, The Clarification part is extremely helpful__ for writing a bug-free solution. It's always better to clarify further about what the question is ask. For example, can we use __String.split()__ and __String.substring()__? (normally we would better not to) Can we use any extra space? That decides weather we copy by substring or by character. 

In conclusion, __this is an easy question that's not easy to get correct answer__. Practise more! And since this is the last post of Leetcode questions, my focus from tomorrow onwards will be shifted to "CC150". Thanks for reading! 

### Code

__My code__. pointer solution. 

    public String reverseWords(String s) {
		if (s.length() == 0) return "";
		int p = s.length() - 1;
		// p points to the last non-space character
		String ans = "";
		while (p >= 0) {
			int j = p;
			while (j >= 0 && s.charAt(j) != ' ') {
				j --;
			}
			ans += s.substring(j + 1, p + 1) + " ";
			p = j;
			while (p >= 0 && s.charAt(p) == ' ') {
				p--;
			}
		}
		return ans.trim();
    }

__Updated on Sep 12th__: updated with 3-step-reverse method.

    public String reverseWords(String s) {
        if (s == null || s.length() == 0) {
            return s;
        }
        StringBuilder ans = new StringBuilder();
        int len = s.length();
        int p = len - 1;
        while (p >= 0) {
            while (p >= 0 && s.charAt(p) == ' ') {
                p--;
            }
            if (p == -1) {
                break;
            }
            StringBuilder word = new StringBuilder();
            while (p >= 0 && s.charAt(p) != ' ') {
                word.append(s.charAt(p));
                p--;
            }
            if (ans.length() == 0) {
                ans.append(word.reverse().toString());
            } else {
                ans.append(" " + word.reverse().toString());
            }
        }
        return ans.toString();
    }
