---
layout: post
title: "[Question] Split an integer or coin"
comments: true
category: Question

---

### Question

[link](http://blog.csdn.net/hackbuteer1/article/details/8035261)

> 整数的拆分问题

> 如，对于正整数n=6，可以拆分为：

    6
    5+1
    4+2, 4+1+1
    3+3, 3+2+1, 3+1+1+1
    2+2+2, 2+2+1+1, 2+1+1+1+1
    1+1+1+1+1+1+1

> 现在的问题是，对于给定的正整数n，程序输出该整数的拆分种类数(HDOJ  1028)。

### Solution 

This is very similar to another question I posted before: __Coin Change Problem__. 

__The DP equation is__: 

> q(n,k) = q(n,k-1) + q(n-k,k)

### Code

__not written by me__

    int main(void) {  
        int n,i,j,dp[121][121];  
        for(i = 1 ; i < 121 ; ++i)  
        {  
            for(j = 1 ; j < 121 ; ++j)  
            {  
                if(i == 1 ||  j == 1)  
                    dp[i][j] = 1;  
                else if(i > j)  
                    dp[i][j] = dp[i][j-1] + dp[i-j][j];  
                else if(i == j)  
                    dp[i][j] = dp[i][j-1] + 1;  
                else  
                    dp[i][j] = dp[i][i];  
            }  
        }  

        while(scanf("%d",&n)!=EOF)  
        {  
            cout<<dp[n][n]<<endl;  
        }  
        return 0;  
    }
