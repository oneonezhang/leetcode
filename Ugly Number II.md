#Ugly Number II
##Problem:
Write a program to find the n-th ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5. For example, 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 is the sequence of the first 10 ugly numbers.

Note that 1 is typically treated as an ugly number.
##Idea:
use the result of `Ugly Number` TLE!!
```cpp
class Solution {
public:
    int nthUglyNumber(int n) {
        int num=1;
        while(n)
        {
            if(isUgly(num)) n--;
            num++;
        }
        return num--;
    }
private:
    bool isUgly(int num)
    {
        while(num%2==0) num/=2;
        while(num%3==0) num/=3;
        while(num%5==0) num/=5;
        return num==1;
    }
};
```
##To Study:
Hint:

1. The naive approach is to call isUgly for every number until you reach the nth one. Most numbers are not ugly. Try to focus your effort on generating only the ugly ones.
2. An ugly number must be multiplied by either 2, 3, or 5 from a smaller ugly number.
3. The key is how to maintain the order of the ugly numbers. Try a similar approach of merging from three sorted lists: L1, L2, and L3.
4. Assume you have Uk, the kth ugly number. Then Uk+1 must be Min(L1 \* 2, L2 \* 3, L3 \* 5).  

`Dynamic Programming`
```cpp
class Solution {
public:
    int nthUglyNumber(int n) {
        vector<int> uglyNums(n);
        uglyNums[0]=1;
        int twoIndex=0,threeIndex=0,fiveIndex=0;
        for(int i=1;i<n;i++)
        {
            uglyNums[i]=min(min(uglyNums[twoIndex]*2,uglyNums[threeIndex]*3),uglyNums[fiveIndex]*5);
            if(uglyNums[twoIndex]*2==uglyNums[i]) twoIndex++;
            if(uglyNums[threeIndex]*3==uglyNums[i]) threeIndex++;
            if(uglyNums[fiveIndex]*5==uglyNums[i]) fiveIndex++;
        }
        return uglyNums[n-1];
    }
};
```