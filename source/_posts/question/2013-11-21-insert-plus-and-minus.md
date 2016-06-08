---
layout: post
title: "[Question] Insert Plus and Minus to Complete Expression "
comments: true
category: Question

---

# Question 

[link](http://www.1point3acres.com/bbs/thread-148692-1-1.html)

> Given a string of numbers, eg. "43868643". Put '+' and '-' in between, and build an expression. 

# Solution

Iterate thru the input string and do DFS recrusively. 

At each position, there's 3 possibilities: plus, minus or do not skip. 

# Code

	public List<String> solve(String str) {
		if (str == null || str.length() == 0) {
			return null;
		}
		List<String> result = new ArrayList<String>();
		helper(result, "", 0, str);
		Collections.sort(result);
		return result;
	}

	private void helper(List<String> result, String curExp, int curVal, String remain) {
		if (curVal == Integer.parseInt(remain)) {
			result.add(curExp + "=" + remain);
		} else if (curVal + Integer.parseInt(remain) == 0) {
			result.add(curExp + "=-" + remain);
		}
		for (int i = 1; i < remain.length(); i++) {
			String nextStr = remain.substring(0, i);
			int nextNum = Integer.parseInt(nextStr);

			// case 1: add a + between curExp and nextStr
			String newExp = curExp + "+" + nextStr;
			int newVal = curVal + nextNum;
			helper(result, newExp, newVal, remain.substring(i));

			// case 2: '-' sign
			newExp = curExp + "-" + nextStr;
			newVal = curVal - nextNum;
			helper(result, newExp, newVal, remain.substring(i));
		}
	}

# Testing

    Input is 4312
    Print the list: 
    +4-3+1=2
    -4+3-1=-2

    Input is 43868643
    Print the list: 
    +4+3+8+6-8-6-4=3
    +4+3+8-6-8+6-4=3
    +4+3+86-86-4=3
    +4+3-8+6+8-6-4=3
    +4+3-8+68-64=3
    +4+3-8-6+8+6-4=3
    +4+3-86+86-4=3
    +4-3+8+6-8-6-4=-3
    +4-3+8-6-8+6-4=-3
    +4-3+86-86-4=-3
    +4-3-8+6+8-6-4=-3
    +4-3-8+68-64=-3
    +4-3-8-6+8+6-4=-3
    +4-3-86+86-4=-3
    +43+8+6-8-6=43
    +43+8-6-8+6=43
    +43+86-86=43
    +43-8+6+8-6=43
    +43-8-6+8+6=43
    +43-86+86=43
    -4+3+8+6-8-6+4=3
    -4+3+8-6-8+6+4=3
    -4+3+8-68+64=3
    -4+3+86-86+4=3
    -4+3-8+6+8-6+4=3
    -4+3-8-6+8+6+4=3
    -4+3-86+86+4=3
    -4-3+8+6-8-6+4=-3
    -4-3+8-6-8+6+4=-3
    -4-3+8-68+64=-3
    -4-3+86-86+4=-3
    -4-3-8+6+8-6+4=-3
    -4-3-8-6+8+6+4=-3
    -4-3-86+86+4=-3
    -43+8+6-8-6=-43
    -43+8-6-8+6=-43
    -43+86-86=-43
    -43-8+6+8-6=-43
    -43-8-6+8+6=-43
    -43-86+86=-43
