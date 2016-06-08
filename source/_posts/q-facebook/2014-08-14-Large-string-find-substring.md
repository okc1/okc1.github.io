---
layout: post
title: "[Facebook] Query Search (HashMap, suffix array) "
comments: true
categories:
- q-facebook
- z-string-search

---

### Question 

[link](http://www.itint5.com/oj/#15)

> 有一个长度为n的字符串str，有非常多的关键字query（长度不超过10），需要判断每个关键字是否是str的子串。

> 注意：query是动态的输入进行查询的，预先并不知道所有的query。

### Solution

__Best idea of the solution is to use Suffix Tree__ and similar alternatives. 

__Solution 1__ is [an nice idea using HashMap](http://www.itint5.com/discuss/27/%E5%BA%94%E8%AF%A5%E6%80%8E%E4%B9%88%E9%A2%84%E5%A4%84%E7%90%86). 

> 我是把所有长度< =10的子串，哈希一下存放到10个哈希表中。

> 至于哈希函数的选取，随便选一个应该都不会超时。

__Solution 2__ is using '__suffix array__'. The most important point of this idea is to only make a substring instance __for every 10 characters__. 

> 只用=10的子串。然后二分查找

> 用=10的字串排序即可，如包含更短的串会使得预处理变成O(10nlg(10n))。 查找的复杂度可能没什么变化，使用<=10会是O(lg(10n))，而只使用=10子串初始化的话，因为可能还要进行短query跟长子串间的前缀比较，复杂度会是O(10lgn)，稍微有点提高。

Which is to say, using substring length == 10, we comsume __less time for pre-processing__, and a little __more time when querying__. 

### Code

__Suffix tree solution from [here](http://www.itint5.com/discuss/203/%E8%B6%85%E7%AE%80%E5%8D%95%E7%9A%84prefix-array-java-code)__, note written by me

    private List<String> prefixList;
    
    // pre-process the large string
    public void initWithString(String str) {
        Set<String> strs = new HashSet<String>();

        for(int i = 0; i < str.length(); ++i) {
            strs.add(str.substring(i, Math.min(str.length(), i + 10)));
        }
        prefixList = new ArrayList<String>(strs);
        Collections.sort(prefixList);
    }
    
    // find the query substring
    public boolean existSubString(String query) {
        int low = 0;
        int high = prefixList.size() - 1;
        while(low <= high) {
            int mid = (low + high) / 2;
            int comp = prefixList.get(mid).compareTo(query);
            if(comp == 0)  {
                return true;
            }
            if(prefixList.get(mid).startsWith(query)) {
                return true;
            }
            if(comp > 0) //mid > query
            {
                high = mid - 1;
            }else{
                low = mid + 1;
            }
        }
        return false;
    }
