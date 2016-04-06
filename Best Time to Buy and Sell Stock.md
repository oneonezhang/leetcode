#Best Time to Buy and Sell Stock
##Problem:
Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.
##Idea:
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if(prices.empty()) return 0;
        int buy=-prices[0];
        int sell=0;
        for(int i=1;i<prices.size();i++)
        {
            sell=max(buy+prices[i],sell);
            buy=max(-prices[i],buy);
        }
        return sell;
    }
};
```
##To Study:
`Kadane's Algorithm`
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if(prices.empty()) return 0;
        int maxProfit=0;
        int maxCurrent=0;
        for(int i=1;i<prices.size();i++)
        {
            maxCurrent=max(0,maxCurrent+prices[i]-prices[i-1]);
            maxProfit=max(maxProfit,maxCurrent);
        }
        return maxProfit;
    }
};
```