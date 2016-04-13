#Burst Balloons
##Problem:
Given n balloons, indexed from 0 to n-1. Each balloon is painted with a number on it represented by array nums. You are asked to burst all the balloons. If the you burst balloon i you will get nums[left] * nums[i] * nums[right] coins. Here left and right are adjacent indices of i. After the burst, the left and right then becomes adjacent.

Find the maximum coins you can collect by bursting the balloons wisely.

Note: 
(1) You may imagine nums[-1] = nums[n] = 1. They are not real therefore you can not burst them.  
(2) 0 ≤ n ≤ 500, 0 ≤ nums[i] ≤ 100

Example:

Given [3, 1, 5, 8]

Return 167

    nums = [3,1,5,8] --> [3,5,8] -->   [3,8]   -->  [8]  --> []  
    coins =  3*1*5      +  3*5*8    +  1*3*8      + 1*8*1   = 167
    
##To Study:
Reverse thinking:
>We divide the problem by the last balloon to burst.We can see that the balloons is again separated into 2 sections. But this time since the balloon i is the last balloon of all to burst, the left and right section now has well defined boundary and do not affect each other

1.`Divide and Conquer with Memoization`:memoization can optimize recursion
```cpp
class Solution {
public:
    int maxCoins(vector<int>& nums) {
        int newArray[nums.size()+2];
        newArray[0]=1;
        int n=1;
        for(int i=0;i<nums.size();i++)
        {
            if(nums[i]>0)//we can skip 0 since it doesn't add coins
            {
                newArray[n]=nums[i];
                n++;
            }
        }
        newArray[n]=1;
        vector<vector<int>> record(n+1,vector<int>(n+1,-1));
        return sub(record,newArray,0,n);
    }
private:
    int sub(vector<vector<int>>& record,int newArray[],int left,int right)
    {
        if(right-left==1) return 0;
        else if(record[left][right]>=0) return record[left][right];
        else
        {
            int maxValue=0;
            for(int i=left+1;i<right;i++)
            {
                maxValue=max(maxValue,newArray[left]*newArray[i]*newArray[right]+sub(record,newArray,left,i)+sub(record,newArray,i,right));
            }
            record[left][right]=maxValue;//Important!Otherwise it will TLE!
            return maxValue;
        }
    }
};
```
2.`Dynamic Programming`
```cpp
class Solution {
public:
    int maxCoins(vector<int>& nums) {
        int newArray[nums.size()+2];
        newArray[0]=1;
        int n=1;
        for(int i=0;i<nums.size();i++)
        {
            if(nums[i]>0)
            {
                newArray[n]=nums[i];
                n++;
            }
        }
        newArray[n]=1;
        int dp[n+1][n+1]={};
        for(int k=2;k<=n;k++)
        {
            for(int left=0;left<=n-k;left++)
            {
                int right=left+k;
                for(int i=left+1;i<right;i++)
                {
                    dp[left][right]=max(dp[left][right],dp[left][i]+dp[i][right]+newArray[i]*newArray[left]*newArray[right]);
                }
            }
        }
        return dp[0][n];
    }
};
```
Time Complexity:O(n^3)