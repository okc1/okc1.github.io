---
layout: post
title: "[LeetCode 68] Text Justification (unsolvable)"
comments: true
category: Leetcode
tags: [ unsolvable ]
---

### Question 

[link](http://oj.leetcode.com/problems/text-justification/)

<div class="question-content">
            <p></p><p>
Given an array of words and a length <i>L</i>, format the text such that each line has exactly <i>L</i> characters and is fully (left and right) justified.
</p> 

<p>
You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces <code>' '</code> when necessary so that each line has exactly <i>L</i> characters.
</p>

<p>
Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line do not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.
</p>

<p>
For the last line of text, it should be left justified and no extra space is inserted between words.
</p>

<p>
For example,<br>
<b>words</b>: <code>["This", "is", "an", "example", "of", "text", "justification."]</code><br>
<b>L</b>: <code>16</code>.
</p>

<p>
Return the formatted lines as:<br>
</p><pre>[
   "This    is    an",
   "example  of text",
   "justification.  "
]
</pre>
<p></p>

<p>
<b>Note:</b> Each word is guaranteed not to exceed <i>L</i> in length.
</p>


<p class="showspoilers"><a href="#" onclick="showSpoilers(this); return false;">click to show corner cases.</a></p>

<div class="spoilers" style="display: none;"><b>Corner Cases:</b>
<p>
</p><ul>
<li>A line other than the last line might contain only one word. What should you do in this case?<br>
In this case, that line should be left-justified.</li>
<p></p>
</ul></div><p></p>
          </div>

### Stats

<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="lime">2</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="red">4</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="red">unsolvable</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">unsolvable</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Solution

I was not able to come up with a solution. 

I found solution in [here](https://github.com/rffffffff007/leetcode/blob/master/Text%20Justification.java), [here](http://blog.csdn.net/linhuanmars/article/details/24063271) and [here](http://gongxuns.blogspot.sg/2012/12/leetcodetext-justification.html). I will post the code from first link. 

### My code

    public ArrayList < String > fullJustify(String[] words, int L) {
        int wordsCount = words.length;
        ArrayList < String > result = new ArrayList < String > ();
        int curLen = 0;
        int lastI = 0;
        for (int i = 0; i <= wordsCount; i++) {
            if (i == wordsCount || curLen + words[i].length() + i - lastI > L) {
                StringBuffer buf = new StringBuffer();
                int spaceCount = L - curLen;
                int spaceSlots = i - lastI - 1;
                if (spaceSlots == 0 || i == wordsCount) {
                    for (int j = lastI; j < i; j++) {
                        buf.append(words[j]);
                        if (j != i - 1)
                            appendSpace(buf, 1);
                    }
                    appendSpace(buf, L - buf.length());
                } else {
                    int spaceEach = spaceCount / spaceSlots;
                    int spaceExtra = spaceCount % spaceSlots;
                    for (int j = lastI; j < i; j++) {
                        buf.append(words[j]);
                        if (j != i - 1)
                            appendSpace(buf, spaceEach + (j - lastI < spaceExtra ? 1 : 0));
                    }
                }
                result.add(buf.toString());
                lastI = i;
                curLen = 0;
            }
            if (i < wordsCount)
                curLen += words[i].length();
        }
        return result;
    }

    private void appendSpace(StringBuffer sb, int count) {
        for (int i = 0; i < count; i++)
            sb.append(' ');
    }
