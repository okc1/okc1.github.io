---
layout: post
title: "[Google] Alphabet Table (`)"
comments: true
category: q-google

---

### Question 

[link](http://blog.sina.com.cn/s/blog_979956cc0101i67x.html)

> 每一种语言，都有自己的字母表，类似英文的a-z，但是顺序不相同。例如，有的语言可能是z是第一个之类的。现在给定这个语言的字典，请分析这个字典，得到这个语言的字母表的顺序。 

> 例如：有如下的字母：C CAC CB BCC BA。 经过分析，得到字母表为C->A->B。

### Solution

http://page.renren.com/601882592/channel-noteshow-927705419

1. C 2. CAC 3. CB 4. BCC 5. BA 经过分析，得到字母表为C->A->B。 

分析 字典序相邻的位置的字符串，只会有如下两种情况： 

（1）排在前面的字符串是下一个串的子串，如C与CAC

（2）两个字符串具有第一对不相同的字符对，如CAC和CBB，第一个不相同的字符对为（A，B），这是就要求A在字母表中的顺序在B前面。对于后面字符并没有要求，如并不要求第二个不相同的字符对（C，B）中的C在字母表中的顺序在B前面。

所以按照第（2）种情况建图，然后对该有向无环图求拓扑排序即可。

So this becomes a Topology Sorting question. 

### Code

__not written by me__

    pair<char,char>  constructEdge(const string & src1, const string & src2)
    {
         int min_len = min(src1.length(), src2.length());
         int i = 0;
         while(i < min_len && src1[i] == src2[i]){
               i++;
         }
         if(i < min_len){
               return  make_pair(src1[i], src2[i]);
         }else{
               return  make_pair('\0','\0');
         }
    }
    //-1, 0, 1
    int  alphaTable(const vector<string> &  dict, vector<char> & alpha_table)
    {
         unordered_map<char,set<char> >  edges;
         set<char> nodes;
         for(const string & word : dict){
              for(char c : word){
                  nodes.insert(c);
              }
         }
         unordered_map<char,int>  in_degree;
         for(int i = 1; i < dict.length(); i++){
              pair edge = constructEdge(dict[i-1],dict[i]);
              if(edge.first != '\0'){
                  edges[edge.first].insert(edge.second);
                  in_degree[edge.second]++;
              }
         }
         queue<char>  q;
         for(char node : nodes){
             if(in_degree[node] == 0){
                  q.push(node);
             }
         }
         alpha_table.clear();
         int result = 0;
         while(!q.empty()){
            if(q.size() > 1){
                result = 1;
            }
            char  c = q.front();
            q.pop();
            alpha_table.push_back(c);
            for(char node : edges[c]){
                 in_degree[node] --;
                 if(in_degree[node] == 0){
                      q.push(node);
                 }
             }
         }//while
         if(alpha_table.size() < nodes.size()){
             result = -1;
         }
         return result;    
    }
