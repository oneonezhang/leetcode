#Climbing Stairs
##Problem:
You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?
##Idea:
`Fibonacci`  
`Dynamic Programming`
```cpp
class Solution {
public:
    int climbStairs(int n) {
        if(n<=1) return 1;
        else
        {
            int sub[n+1];
            sub[0]=1;
            sub[1]=1;
            for(int i=2;i<=n;i++)
            {
                sub[i]=sub[i-1]+sub[i-2];
            }
            return sub[n];
        }
    }
};
```
##To Study:
We can use two varibles `oneStepBefore`, `twoStepBefore` instead of an array to decrease space complexity.
```cpp
class Solution {
public:
    int climbStairs(int n) {
        int result=1;
        if(n>=2)
        {
            int oneStepBefore=1;
            int twoStepBefore=1;
            for(int i=2;i<=n;i++)
            {
                result=oneStepBefore+twoStepBefore;
                twoStepBefore=oneStepBefore;
                oneStepBefore=result;
            }
        }
        return result;
    }
};
```