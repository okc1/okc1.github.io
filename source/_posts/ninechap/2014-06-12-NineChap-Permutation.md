---
layout: post
title: "[NineChap 1.2] Permutation"
comments: true
category: NineChap

---


## First Word

Permutation questions provide you with a list of items, and you build, validate and return a combination of these items. The standard solution is to sort the input first, and add items 1 by 1. 

__Do not try to solve the problems with anything other than the template given below__, because otherwise the code is impossible to be bug-free. 

Though the code is standard, __many question are very difficult__, and most of time __duplication removal can be tough__. 

## Template

    public List<List<Integer>> subsets(int[] num) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        if(num == null || num.length == 0) {
            return result;
        }
        Arrays.sort(num);  
        subsetsHelper(result, new ArrayList<Integer>(), num, 0);
        return result;
    }

    private void subsetsHelper(List<List<Integer>> result,
        List<Integer> list, int[] num, int pos) {
        result.add(new ArrayList<Integer>(list));
        for (int i = pos; i < num.length; i++) {
            list.add(num[i]);
            subsetsHelper(result, list, num, i + 1);
            list.remove(list.size() - 1);
        }
    }

__Note:__ 2nd last line "subsetsHelper(result, list, num, i + 1);". 

It's easy to mistake it as "pos+1" instead of "i+1", which will result in TLE.

## Question list

1. __[Subsets]({% post_url /leetcode/2014-05-22-Subsets %})__

1. __[Permutations]({% post_url /leetcode/2014-05-14-Permutations %})__

1. __[Subsets II]({% post_url /leetcode/2014-05-22-Subsets-II %})__

1. __[Permutations II]({% post_url /leetcode/2014-05-14-Permutations-II %})__

#### Additional

1. __[Combination Sum]({% post_url /leetcode/2014-05-13-Combination-Sum %})__

1. __[Combination Sum II]({% post_url /leetcode/2014-05-13-Combination-Sum-II %})__

1. __[Palindrome Partitioning]({% post_url /leetcode/2014-05-29-Palindrome-Partitioning %})__

1. __[Palindrome Partitioning II]({% post_url /leetcode/2014-05-30-Palindrome-Partitioning-II %})__

1. __[Restore IP Addresses]({% post_url /leetcode/2014-05-24-Restore-IP-Addresses %})__

1. __[Combinations]({% post_url /leetcode/2014-05-22-Combinations %})__

1. __[Letter Combinations of a Phone Number]({% post_url /leetcode/2014-05-02-Letter-Combinations-of-a-Phone-Number %})__

## Code

__Subsets__ - good example for practise (by applying the model)

    public List<List<Integer>> subsets(int[] num) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        if(num == null || num.length == 0) {
            return result;
        }
        Arrays.sort(num);
        helper(result, new LinkedList<Integer>(), num, 0);
        return result;
    }
    
    private void helper(List<List<Integer>> ans, List<Integer> path, int[] num, int position) {
        ans.add(new LinkedList<Integer>(path));
        for (int i = position; i < num.length; i ++) {
            path.add(num[i]);
            helper(ans, path, num, i + 1);
            path.remove(path.size() - 1);
        }
    }

__Permutations__

    public List<List<Integer>> permute(int[] num) {
        List<List<Integer>> ans = new LinkedList<List<Integer>>();
        if (num == null || num.length == 0) {
            return ans;
        }
        helper(ans, new LinkedList<Integer>(), num);
        return ans;
    }
    
    private void helper(List<List<Integer>> ans, List<Integer> path, int[] num){
        if (path.size() == num.length) {
            ans.add(new LinkedList<Integer>(path));
            return;
        }
        for (int i = 0; i < num.length; i ++) {
            if (!path.contains(num[i])) {
                path.add(num[i]);
                helper(ans, path, num);
                path.remove(path.size() - 1);
            }
        }
    }

__Subsets II__ - good example for practise

We only care how many times we use the duplicate number, we care not the order. So, only 3 lines of code is added based on previous solution. 

    public List<List<Integer>> subsetsWithDup(int[] num) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        if(num == null || num.length == 0) {
            return result;
        }
        Arrays.sort(num);
        helper(result, new LinkedList<Integer>(), num, 0);
        return result;
    }
    
    private void helper(List<List<Integer>> ans, List<Integer> path, int[] num, int position) {
        ans.add(new LinkedList<Integer>(path));
        for (int i = position; i < num.length; i ++) {
            if (i > position && num[i - 1] == num[i]) {
                // if duplicate, only append num[position]
                continue;
            }
            path.add(num[i]);
            helper(ans, path, num, i + 1);
            path.remove(path.size() - 1);
        }
    }

__Permutations II__

    public List<List<Integer>> permuteUnique(int[] num) {
        List<List<Integer>> ans = new LinkedList<List<Integer>>();
        if (num == null || num.length == 0) {
            return ans;
        }
        Arrays.sort(num);
        helper(ans, new LinkedList<Integer>(), new int[num.length], num);
        return ans;
    }
    
    private void helper(List<List<Integer>> ans, List<Integer> path, int[] visited, int[] num){
        if (path.size() == num.length) {
            ans.add(new LinkedList<Integer>(path));
            return;
        }
        for (int i = 0; i < num.length; i ++) {
            if (visited[i] == 1) {
                continue;
            }
            if (i > 0 && visited[i-1] == 0 && num[i - 1] == num[i]) {
                continue;
            }
            visited[i] = 1;
            path.add(num[i]);
            helper(ans, path, visited, num);
            visited[i] = 0;
            path.remove(path.size() - 1);
        }
    }

__Combination Sum__

    public ArrayList<ArrayList<Integer>> combinationSum(int[] candidates, int target) {
        ArrayList<ArrayList<Integer>> ans = new ArrayList<ArrayList<Integer>>();
        Arrays.sort(candidates);
        helper(ans, new ArrayList<Integer>(), candidates, 0, target);
        return ans;
    }
    
    private void helper(ArrayList<ArrayList<Integer>> ans, ArrayList<Integer> path, 
                        int[] nums, int pos, int target) {
        if (target < 0) {
            return;
        } else if (target == 0) {
            ans.add(new ArrayList<Integer>(path));
            return;
        }
        for (int i = pos; i < nums.length; i ++) {
            path.add(nums[i]);
            helper(ans, path, nums, i, target - nums[i]);
            path.remove(path.size() - 1);
        }
    }

__Combination Sum II__

    public ArrayList<ArrayList<Integer>> combinationSum2(int[] candidates, int target) {
        ArrayList<ArrayList<Integer>> ans = new ArrayList<ArrayList<Integer>>();
        Arrays.sort(candidates);
        helper(ans, new ArrayList<Integer>(), candidates, 0, target);
        return ans;
    }
    
    private void helper(ArrayList<ArrayList<Integer>> ans, ArrayList<Integer> path, 
                        int[] nums, int pos, int target) {
        if (target < 0) {
            return;
        } else if (target == 0) {
            ans.add(new ArrayList<Integer>(path));
            return;
        }
        for (int i = pos; i < nums.length; i ++) {
            if (i > pos && nums[i-1] == nums[i]) {
                continue;
            }
            path.add(nums[i]);
            helper(ans, path, nums, i + 1, target - nums[i]);
            path.remove(path.size() - 1);
        }
    }

__Palindrome Partitioning__

Naive approach can AC:

    public ArrayList<ArrayList<String>> partition(String s) {
        ArrayList<ArrayList<String>> ans = new ArrayList<ArrayList<String>>();
        if (s == null || s.length() == 0) {
            return ans;
        }
        helper(ans, new ArrayList<String>(), s, 0);
        return ans;
    }

    private void helper(ArrayList<ArrayList<String>> ans, ArrayList<String> path, String s, int pos) {
        if (pos == s.length()) {
            ans.add(new ArrayList<String>(path));
            return;
        }
        for (int i = pos + 1; i <= s.length(); i++) {
            String sub = s.substring(pos, i);
            if (!isPlm(sub)) {
                continue;
            }
            path.add(sub);
            helper(ans, path, s, i);
            path.remove(path.size() - 1);
        }
    }

    private boolean isPlm(String str) {
        int left = 0, right = str.length() - 1;
        while (left < right) {
            if (str.charAt(left) != str.charAt(right)) 
                return false;
            left++;
            right--;
        }
        return true;
    }

Use DP to optimize the process of palindrome validation. 

    // palindrome validation optimized with DP
    public ArrayList<ArrayList<String>> partition(String s) {
        ArrayList<ArrayList<String>> ans = new ArrayList<ArrayList<String>>();
        if (s == null || s.length() == 0) {
            return ans;
        }
        helper(ans, new ArrayList<String>(), s, 0, palindromeMap(s));
        return ans;
    }

    private void helper(ArrayList<ArrayList<String>> ans, 
    ArrayList<String> path, String s, int pos, boolean[][] palinMap) {
        if (pos == s.length()) {
            ans.add(new ArrayList<String>(path));
            return;
        }
        for (int i = pos; i < s.length(); i++) {
            if (!palinMap[i][pos]) {
                continue;
            }
            path.add(s.substring(pos, i + 1));
            helper(ans, path, s, i + 1, palinMap);
            path.remove(path.size() - 1);
        }
    }
    
    private boolean[][] palindromeMap(String s) {
        int len = s.length();
        boolean[][] map = new boolean[len][len];
        char[] ss = s.toCharArray();
        for (int i = 0; i < len; i++) {
            for (int j = i; j >= 0; j--) {
                if (i == j) {
                    map[i][j] = true;
                } else if (i - j == 1) {
                    map[i][j] = ss[i] == ss[j];
                } else {
                    map[i][j] = (ss[i] == ss[j]) & map[i - 1][j + 1];
                }
            }
        }
        return map;
    }

__Palindrome Partitioning II__

Used above template and got TLE. Turns out, this is a pure DP question. 

Skip for now. 

__Restore IP Addresses__

    public List<String> restoreIpAddresses(String s) {
        List<String> ans = new LinkedList<String>();
        if (s == null || s.length() == 0) {
            return ans;
        }
        helper(ans, s, "", 0, 0);
        return ans;
    }
    
    private void helper(List<String> ans, String s, String path, int pos, int count) {
        if (count == 4) {
            if (pos == s.length()) {
                ans.add(path.substring(1));
            }
            return;
        }
        for (int i = pos; i < s.length(); i++) {
            if (i - pos >= 3) {
                break;
            }
            if (!isValidNum(s.substring(pos, i + 1))) {
                continue;
            }
            String newPath = path + "." + s.substring(pos, i + 1);
            helper(ans, s, newPath, i + 1, count + 1);
        }
    }
    
    private boolean isValidNum(String str) {
        if (str.length() > 1 && str.charAt(0) == '0') {
            return false;
        }
        int num = Integer.parseInt(str);
        if (num < 0 || 255 < num) {
            return false;
        }
        return true;
    }

__Combinations__

    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> ans = new LinkedList<List<Integer>>();
        if (n == 0 || k == 0 || n < k) {
            return ans;
        }
        helper(ans, new LinkedList<Integer>(), n, k, 1);
        return ans;
    }
    
    private void helper(List<List<Integer>> ans, List<Integer> path, int n, int k, int pos) {
        if (path.size() == k) {
            ans.add(new LinkedList<Integer>(path));
            return;
        }
        for (int i = pos; i <= n; i++) {
            path.add(i);
            helper(ans, path, n, k, i + 1);
            path.remove(path.size() - 1);
        }
    }

__Letter Combinations of a Phone Number__

    public List<String> letterCombinations(String digits) {
        List<String> ans = new LinkedList<String>();
        if (digits == null) {
            return ans;
        }
        String[] pad = new String[]{
            " ","","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
        helper(ans, "", pad, digits, 0);
        return ans;
    }
    
    private void helper(List<String> ans, String path, String[] pad, String digits, int pos) {
        if (path.length() == digits.length()) {
            ans.add(path);
            return;
        }
        String letters = pad[digits.charAt(pos) - '0'];
        for (int i = 0; i < letters.length(); i++) {
            path += letters.charAt(i) + "";
            helper(ans, path, pad, digits, pos + 1);
            path = path.substring(0, path.length() - 1);
        }
    }

## Conclusion

#### Remember the model! It applies to most search question. 
