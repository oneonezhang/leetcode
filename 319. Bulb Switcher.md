#Bulb Switcher
##Problem:
There are n bulbs that are initially off. You first turn on all the bulbs. Then, you turn off every second bulb. On the third round, you toggle every third bulb (turning on if it's off or turning off if it's on). For the ith round, you toggle every i bulb. For the nth round, you only toggle the last bulb. Find how many bulbs are on after n rounds.

Example:

>Given n = 3.   
>  
>At first, the three bulbs are [off, off, off].  
>After first round, the three bulbs are [on, on, on].  
>After second round, the three bulbs are [on, off, on].  
>After third round, the three bulbs are [on, off, off].    
>  
>So you should return 1, because there is only one bulb is on.  

##Idea：
首先试着统计每盏灯泡的因数个数，因数的奇偶性决定最后是开还是关。
```cpp
class Solution {
public:
    int bulbSwitch(int n) {
        int count=0;
        for(int i=1;i<=n;i++)
        {
            int factorCount=0;
            for(int j=1;i<=sqrt(i);j++)
            {
                if(i%j==0) 
                {
                    factorCount += 2;
                    if(j==sqrt(i)) factorCount -= 1;
                }
            }
            count += factorCount%2;
        }
        return count;
    }
};
```
**但是结果Time Limit Exceeded**     
`In fact,the code above shows that factors of the numbers except square numbers appear in pairs, so the the number of bulbs on is equal to the number of square numbers within n.` 
```cpp
class Solution {
public:
    int bulbSwitch(int n) {
        return floor(sqrt(n));
    }
};
```