---
layout: post
title: "[LeetCode 76] Minimum Window Substring"
comments: true
category: Leetcode

---

### Question 
[link](https://oj.leetcode.com/problems/minimum-window-substring/)

<div class="question-content">
            <p></p><p>
Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).
</p>

<p>
For example,<br>
<b>S</b> = <code>"ADOBECODEBANC"</code><br>
<b>T</b> = <code>"ABC"</code><br>
</p>
<p>
Minimum window is <code>"BANC"</code>.
</p>

<p>
<b>Note:</b><br>
If there is no such window in S that covers all characters in T, return the emtpy string <code>""</code>.
</p>
<p>
If there are multiple such windows, you are guaranteed that there will always be only one unique minimum window in S.
</p><p></p>
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
		<td bgcolor="red">5</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

__This is a very difficult string matching question__. 

The sliding window solution is very well explained in [this post](http://leetcode.com/2010/11/finding-minimum-window-in-s-which.html) (the best solution). 

<blockquote cite="http://fisherlei.blogspot.sg/2013/01/leetcode-simplify-path.html">
    <p>To help illustrate this approach, I use a different example: <b>S</b> = “<b>acbbaca</b>” and <b>T</b> = “<b>aba</b>“. The idea is mainly based on the help of two pointers (begin and end position of the window) and two tables (<i>needToFind </i>and <i>hasFound</i>) while traversing <b>S</b>. <i>needToFind</i> stores the total count of a character in <b>T</b> and <i>hasFound</i> stores the total count of a character met so far. We also use a <i>count</i> variable to store the total characters in <b>T</b> that’s met so far (not counting characters where hasFound[<i>x</i>]<i> </i>exceeds needToFind[<i>x</i>]). When count equals <b>T</b>‘s length, we know a valid window is found.</p><p>Each time we advance the end pointer (pointing to an element <i>x</i>), we increment hasFound[<i>x</i>] by one. We also increment <i>count </i>by one if hasFound[<i>x</i>] is less than or equal to needToFind[<i>x</i>]. Why? When the constraint is met (that is, <i>count</i> equals to <b>T</b>‘s size), we immediately advance begin pointer as far right as possible while maintaining the constraint.</p><p>How do we check if it is maintaining the constraint? Assume that begin points to an element <i>x</i>, we check if hasFound[<i>x</i>] is greater than needToFind[<i>x</i>]. If it is, we can decrement hasFound[<i>x</i>] by one and advancing begin pointer without breaking the constraint. On the other hand, if it is not, we stop immediately as advancing begin pointer breaks the window constraint.</p><p>Finally, we check if the minimum window length is less than the current minimum. Update the current minimum if a new minimum is found.</p><p>Essentially, the algorithm finds the first window that satisfies the constraint, then continue maintaining the constraint throughout.</p><p></p><div class="separator" style="clear: both; text-align: center;"><a href="http://2.bp.blogspot.com/_UElib2WLeDE/TOBuvjG6exI/AAAAAAAACYE/uludVXtJ8OY/s1600/sliding.gif" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" height="83" src="http://2.bp.blogspot.com/_UElib2WLeDE/TOBuvjG6exI/AAAAAAAACYE/uludVXtJ8OY/s400/sliding.gif" width="400"></a></div><div style="text-align: center;"><span style="font-size: x-small;">i) <b>S</b> = “<b>acbbaca</b>” and <b>T</b> = “<b>aba</b>“.<br></span></div><p></p><div class="separator" style="clear: both; text-align: center;"><a href="http://4.bp.blogspot.com/_UElib2WLeDE/TOBvHRLbOAI/AAAAAAAACYI/38QLgUIMePU/s1600/sliding_2.gif" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" height="79" src="http://4.bp.blogspot.com/_UElib2WLeDE/TOBvHRLbOAI/AAAAAAAACYI/38QLgUIMePU/s400/sliding_2.gif" width="400"></a></div><div style="text-align: center;"><span style="font-size: x-small;">ii) The first minimum window is found. Notice that we cannot advance begin pointer as hasFound['a'] == needToFind['a'] == 2. Advancing would mean breaking the constraint.<br></span></div><p></p><div class="separator" style="clear: both; text-align: center;"><a href="http://3.bp.blogspot.com/_UElib2WLeDE/TOBvLH1aLcI/AAAAAAAACYM/pbJLl7qoduo/s1600/sliding_3.gif" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" height="79" src="http://3.bp.blogspot.com/_UElib2WLeDE/TOBvLH1aLcI/AAAAAAAACYM/pbJLl7qoduo/s400/sliding_3.gif" width="400"></a></div><div style="text-align: center;"><span style="font-size: x-small;">iii) The second window is found. begin pointer still points to the first element ‘a’. hasFound['a'] (<b>3</b>) is greater than needToFind['a'] (<b>2</b>). We decrement hasFound['a'] by one and advance begin pointer to the right.<br></span></div><p></p><div class="separator" style="clear: both; text-align: center;"><a href="http://2.bp.blogspot.com/_UElib2WLeDE/TOBvOljpz0I/AAAAAAAACYQ/TxuWgWGTOF4/s1600/sliding_4.gif" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" height="79" src="http://2.bp.blogspot.com/_UElib2WLeDE/TOBvOljpz0I/AAAAAAAACYQ/TxuWgWGTOF4/s400/sliding_4.gif" width="400"></a></div><div style="text-align: center;"><span style="font-size: x-small;">iv) We skip ‘c’ since it is not found in <b>T</b>. Begin pointer now points to ‘b’. hasFound['b'] (<b>2</b>) is greater than needToFind['b'] (<b>1</b>). We decrement hasFound['b'] by one and advance begin pointer to the right.<br></span></div><p></p><div class="separator" style="clear: both; text-align: center;"><a href="http://2.bp.blogspot.com/_UElib2WLeDE/TOBvSOl6RdI/AAAAAAAACYU/R4O1dPXVvBQ/s1600/sliding_5.gif" imageanchor="1" style="margin-left: 1em; margin-right: 1em;"><img border="0" height="79" src="http://2.bp.blogspot.com/_UElib2WLeDE/TOBvSOl6RdI/AAAAAAAACYU/R4O1dPXVvBQ/s400/sliding_5.gif" width="400"></a></div><div style="text-align: center;"><span style="font-size: x-small;">v) Begin pointer now points to the next ‘b’. hasFound['b'] (1) is equal to needToFind['b'] (1). We stop immediately and this is our newly found minimum window.<br></span></div><p>Both the begin and end pointers can advance at most <i>N</i> steps (where <i>N</i> is <b>S</b>‘s size) in the worst case, adding to a total of 2<i>N</i> times. Therefore, the run time complexity must be in <i>O</i>(<i>N</i>).</p>
</blockquote>

### Solution

Best code is from [this post](http://answer.ninechapter.com/solutions/minimum-window-substring/). 

First of all, keep a HashMap to store all letters and occurrance. Then declare a 'count' variable. This is an important varaible. It helps us to check whether we have successfully achieve at least 1 window. After we found the first window, the 'count' variable shall always equals to total number of letters in 'T'. 

Now the looping part. Basically we assume that the window end at one point, and we find the correct starting position and calculate corresponding length. 

The coding part is very difficult. Try to practise more. 

### Code

__Updated on July 7th__, code: 

    public String minWindow(String S, String T) {
        HashMap<Character, Integer> map = new HashMap<Character, Integer>();
        HashMap<Character, Integer> map2 = new HashMap<Character, Integer>();
        for (Character ch: T.toCharArray()) {
            if (map.containsKey(ch)) {
                map.put(ch, map.get(ch) + 1);
            } else {
                map.put(ch, 1);
                map2.put(ch, 0);
            }
        }
        int count = 0;
        int start = 0;
        int end = 0;
        String result = "";
        while (end < S.length()) {
            char cur = S.charAt(end);
            if (!map.containsKey(cur)) {
                end++;
                continue;
            }
            map2.put(cur, map2.get(cur) + 1);
            if (map2.get(cur) <= map.get(cur)) {
                count++;
            }
            
            if (count == T.length()) {
                // locate start point
                while(true) {
                    char ll = S.charAt(start);
                    if (!map.containsKey(ll)) {
                        start++;
                        continue;
                    }
                    if (map2.get(ll) > map.get(ll)) {
                        map2.put(ll, map2.get(ll) - 1);
                        start++;
                        continue;
                    } else {
                        break;
                    }
                }
                if (result.equals("") || result.length() > end - start + 1) {
                    result = S.substring(start, end + 1);
                }
            }
            end++;
        }
        return result;
    }

__Updated on July 19th__, rewrite the code changing all while-loop to for-loop: 

    public String minWindow(String S, String T) {
        if (S.length() < T.length()) {
            return "";
        }
        HashMap<Character, Integer> map = new HashMap<Character, Integer>();
        HashMap<Character, Integer> found = new HashMap<Character, Integer>();
        for (Character ch: T.toCharArray()) {
            if (map.containsKey(ch)) {
                map.put(ch, map.get(ch) + 1);
            } else {
                map.put(ch, 1);
                found.put(ch, 0);
            }
        }
        
        String window = S;
        int count = 0;
        int start  = 0;
        
        char[] letters = S.toCharArray();
        for (int i = 0; i < letters.length; i++) {
            char ch  = letters[i];
            if (!map.containsKey(ch)) {
                continue;
            }
            if (found.get(ch) < map.get(ch)) {
                count++;
            }
            found.put(ch, found.get(ch) + 1);
            if (count == T.length()) {
                // update the start pointer
                for (; start <= i; start++) {
                    char sChar = letters[start];
                    if (!map.containsKey(sChar)) {
                        continue;
                    }
                    if (found.get(sChar) <= map.get(sChar)) {
                        break;
                    } else {
                        found.put(sChar, found.get(sChar) - 1);
                    }
                }
                if (window.length() > i - start + 1) {
                    window = S.substring(start, i + 1);
                }
            }
        }
        return count == T.length() ? window : "";
    }
