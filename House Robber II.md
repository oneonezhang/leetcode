#House Robber II
##Problem:
Note: This is an extension of House Robber.

After robbing those houses on that street, the thief has found himself a new place for his thievery so that he will not get too much attention. This time, all houses at this place are arranged in a circle. That means the first house is the neighbor of the last one. Meanwhile, the security system for these houses remain the same as for those in the previous street.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.
##Idea:
Either the first one or the last one isn't robbed.
```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        int n=nums.size();
        if(n==0) return 0;
        if(n==1) return nums[0];
        
        vector<int> notRobFirst(n);
        vector<int> notRobLast(n);
        notRobFirst[0]=0;
        notRobFirst[1]=nums[1];
        notRobLast[0]=nums[0];
        notRobLast[1]=(nums[1]>nums[0])?nums[1]:nums[0];
        
        for(int i=2;i<n-1;i++)
        {
            notRobFirst[i]=max(notRobFirst[i-1],notRobFirst[i-2]+nums[i]);
            notRobLast[i]=max(notRobLast[i-1],notRobLast[i-2]+nums[i]);            
        }
        notRobFirst[n-1]=max(notRobFirst[n-2],notRobFirst[n-3]+nums[n-1]);
        notRobLast[n-1]=notRobLast[n-2];
        
        return max(notRobFirst[n-1],notRobLast[n-1]);
    }
};
```