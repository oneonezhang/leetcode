#Best Time to Buy and Sell Stock II
##Problem:
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
##Idea:
When the stock is going to rise,buy!  
When the stock is going to fall,sell!
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int buyprice;
        int profit=0;
        bool have=0;
        if(prices.empty()) return 0;
        for(int i=0;i<prices.size()-1;i++)
        {
            switch(have)
            {
                case 0:
                {
                    if(prices[i]<prices[i+1])
                    {
                        buyprice=prices[i];
                        have=1;
                    }
                    break;
                }
                case 1:
                {
                    if(prices[i]>prices[i+1])
                    {
                        profit += prices[i]-buyprice;
                        have=0;
                    }
                    break;
                }
            }
        }
        if(have==1&&(prices.back()>buyprice))
        {
            profit += prices.back()-buyprice;
            have=0;
        }
        return profit;    
    }
};
```
##To Study:
[1,5,7] 7-1=(5-1)+(7-5)  
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int profit=0;
        int n=prices.size();
        for(int i=0;i<n-1;i++)
        {
            if(prices[i+1]>prices[i])
                profit += prices[i+1]-prices[i];
        }
        return profit;    
    }
};
```