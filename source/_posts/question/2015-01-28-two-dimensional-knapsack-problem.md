---
layout: post
title: "[Question] Two Dimensional Knapsack Problem"
comments: true
category: Question
tags: [ unit test needed ]
---

### Question 

[link](http://blog.sina.com.cn/s/blog_8a24b3a3010190ak.html)

> 给定n种物品和一背包。物品i的重量是wi，体积是bi，其价值为vi，背包的容量为C，容积为D。问应如何选择装入背包中的物品，使得装入背包中物品的总价值最大？

> 在选择装入背包的物品时，对每种物品i只有两种选择，即装入背包或者不装入背包。不能将物品i装入背包多次，也不能只装入部分的物品i。试设计一个解此问题的动态规划算法，并分析算法的计算复杂性。

### Analysis

This is a extended question from __[Question] 0-1 Knapsack Problem__. 

Same solution, just use 3D-array for DP. 

### Solution

First of all, define a 2D array, Knapsack(n,W) denotes getting 'n'th item, with weight 'W'. When n == 0 or W = 0, dp value is 0. 

> int[][][] dp = new int[n + 1][W + 1][B + 1];

Now if item 'n' is able to fit in:

> dp[i][j][k] = max(dp[i-1][j][k] , dp[i-1][j-w[i]][k-b[i]] + v[i]);

If not able to fit in: 

> dp[i][j][k] = dp[i-1][j][k];

### Code

Code from [绝对快乐一生](http://blog.sina.com.cn/s/blog_8a24b3a3010190ak.html): 

    int main()
    {
       int i,j,k;
       int n,c,d;
       int w[MAX] = {0};   //重量
       int b[MAX] = {0};   //体积
       int v[MAX] = {0};   //价值
       cout<<"请输入物品个数:";
       cin>>n;
       cout<<"请输入背包的容量及容积:";
       cin>>c>>d;
       cout<<"请依次输入各个物品的重量,体积,价值:(共"<<n<<"个)"<<endl;
       for(i =1;i<n+1;i++)
       {
           cin>>w[i]>>b[i]>>v[i];
       }

       int dp[50][50][50]={0}; 
       //dp[i][j][k] i代表着第1到第i个物品，j代表的是重量，k代表的是容积，dp为最优价值

       for(i=1;i<n+1;i++)
           for(j =1;j <=c;j++)
               for(k = 1 ;k <= d ; k++)
               {
                   if(w[i]<=j&&b[i]<=k)  
                   //当前物品重量小于当前容量，且体积小于容积时 ，才可以考虑装入物品的问题
                       dp[i][j][k] = max(dp[i-1][j][k] , dp[i-1][j-w[i]][k-b[i]] + v[i]);
                   else dp[i][j][k] = dp[i-1][j][k];
               }
       cout<<"背包能放物品的最大价值为:"<<dp[n][c][d]<<endl;
      int x[MAX] ={0};   //记录是否被选中
      for(i =n;i>1;i--)
           if(dp[i][c][d]==dp[i-1][c][d])x[i] =0;
          else {x[i]=1;c -= w[i];d -= b[i];}
       x[1]=(dp[1][c][d])?1:0;
       cout<<"被选入背包的物品的编号,质量和体积,价值分别是:"<<endl;
       for(i=1;i<</span>n+1;i++)
           if(x[i]==1)
               cout<<"第"<<i<<"个物品: "<<w[i]<<"  "<<b[i]<<"  "<<v[i]<<endl;

    }
