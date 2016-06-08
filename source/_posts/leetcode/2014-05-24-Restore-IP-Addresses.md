---
layout: post
title: "[LeetCode 93] Restore IP Addresses"
comments: true
category: Leetcode

---


### Question 
[link](https://oj.leetcode.com/problems/restore-ip-addresses/)

<div class="question-content">
            <p></p><p>Given a string containing only digits, restore it by returning all possible valid IP address combinations.</p>

<p>
For example:<br>
Given <code>"25525511135"</code>,
</p>
<p>
return <code>["255.255.11.135", "255.255.111.35"]</code>. (Order does not matter)
</p><p></p>
          </div>

### Stats
<table border="2">
	<tr>
		<td>Frequency</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Adjusted Difficulty</td>
		<td bgcolor="yellow">3</td>
	</tr>
	<tr>
		<td>Time to use</td>
		<td bgcolor="red">----------</td>
	</tr>
</table>

Ratings/Color = 1(white) 2(lime) 3(yellow) 4/5(red)

### Analysis

This is question can be solved by __either DFS or Brute Force__, both are fine. 

### Solution

__The DFS solution is obvious, I have the code for it__. 

However, there's [another person](http://blog.csdn.net/u011095253/article/details/9158449) who wrote much less code while implementing the same solution as mine. I will post his code as a good example to learn. 

__The brute force solution in this case__ does not sound like a bad idea. This is the __most top-rated idea on [official forum](https://oj.leetcode.com/discuss/77/restore-ip-addresses)__ as well. 

>  You can get points' positions by i, j, k. Using these positions, you can divide s into candidate ip-form. Then, you can judge whether the candidate fits ip. To improve the efficiency, you can narrow the scope of i, j, k. 

So, this BF code is also posted below. 

Just one more thing. I tested the __exact same BF code written in C++__. Compared to the __420ms__ it took Java to pass OJ test, C++ takes __8ms__ only! I was a bit shocked.

### Code

__First, DFS, my code__

Note: I could have just insert as string, so that convert() method would not be needed. 

    public ArrayList<String> restoreIpAddresses(String s) {
        ArrayList<String> ans = new ArrayList<String>();
        helper(ans, new ArrayList<String>(), s, 0);
        return ans;
    }
    
    private void helper(ArrayList<String> ans, ArrayList<String> cur, String s, int from) {
        int len = s.length();
        if (from >= len) return;
        if (cur.size() == 3) {
            String lastStr = s.substring(from);
            if (isValidIpNumber(lastStr)) {
                ArrayList<String> oneAns = new ArrayList<String>(cur);
                oneAns.add(lastStr);
                ans.add(convert(oneAns));
            }
        }
        else {
            // cur.size less than 3, so get next num (length = 1, 2 or 3)
            for (int i = 1; i <= 3 && from + i <= len; i ++) {
                String nextStr = s.substring(from, from + i);
                if (isValidIpNumber(nextStr)) {
                    cur.add(nextStr);
                    helper(ans, cur, s, from + i);
                    cur.remove(cur.size() - 1);
                }
            }
        }
    }
    
    private boolean isValidIpNumber(String str) {
        if (str.length() == 0 || str.length() > 3) return false;
        if (str.charAt(0) == '0' && str.length() != 1) return false;
        int num = Integer.parseInt(str);
        return (0 <= num && num <= 255);
    }
    
    private String convert(ArrayList<String> l) {
        String ans = "";
        for (String a: l)
            ans += "." + a;
        return ans.substring(1);
    }

__Second, DFS, shorter version code__

    public ArrayList<String> restoreIpAddresses(String s) {
        ArrayList<String> res = new ArrayList<String>();  
        if (s.length()<4||s.length()>12) return res;  
        dfs(s,"",res,0);  
        return res;  
    }  
      
    public void dfs(String s, String tmp, ArrayList<String> res, int count){  
        if (count == 3 && isValid(s)) {  
            res.add(tmp + s);  
            return;  
        }  
        for(int i=1; i<4 && i<s.length(); i++){  
            String substr = s.substring(0,i);  
            if (isValid(substr)){  
                dfs(s.substring(i), tmp + substr + '.', res, count+1);  
            }  
        }  
    }  
      
    public boolean isValid(String s){  
        if (s.charAt(0)=='0') return s.equals("0");  
        int num = Integer.parseInt(s);  
        return num<=255 && num>0;  
    }  

__Third, BF code using triple nested loop (Java)__

    public ArrayList<String> restoreIpAddresses(String s) {
        ArrayList<String> res = new ArrayList<String>();  
        if (s.length() > 12 || s.length() < 4) return res;
        for (int i = 1; i < 4; i ++) {
            String first = s.substring(0, i);
            if (! isValid(first)) continue;
            for (int j = 1; i + j < s.length() && j < 4; j ++) {
                String second = s.substring(i, i + j);
                if (! isValid(second)) continue;
                for (int k = 1; i + j + k < s.length() && k < 4; k ++) {
                    String third = s.substring(i + j, i + j + k);
                    String fourth = s.substring(i + j + k);
                    if (isValid(third) && isValid(fourth)) 
                        res.add(first + "." + second + "." + third + "." + fourth);
                }
            }
        }
        return res;
    }  
      
    public boolean isValid(String s) {
        if (s.length() > 1 && s.charAt(0) == '0') return false;
        return 0 <= Integer.parseInt(s) && Integer.parseInt(s) <= 255;  
    }

__Fourth, same BF code (C++)__

    vector<string> restoreIpAddresses(string s) {
        vector<string> res;
        if (s.size() > 12 || s.size() < 4) return res;
        for (int i=1; i<4; i++) {
            string first = s.substr(0, i);
            if (!isValid(first)) continue;
            for (int j=1; i+j < s.size() && j<4; j++) {
                string second = s.substr(i, j);
                if (!isValid(second)) continue;
                for (int k=1; i+j+k < s.size() && k<4; k++) {
                    string third = s.substr(i+j, k);
                    string fourth = s.substr(i+j+k);
                    if (isValid(third) && isValid(fourth)) {
                        string temp = first+"."+second+"."+third+"."+fourth;
                        res.push_back(temp);
                    }
                }
            }
        }
        return res;
    }
    
    bool isValid(string s) {
        if (s.size() > 1 && s[0] == '0') return false;
        if (stoi(s) <= 255 && stoi(s) >= 0) return true;
        else return false;
    }
