#House Robber
##Problem:
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

#Idea:
`Dynamic programming`
```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        if(!nums.size()) return 0;
        vector<int> money(nums.size());
        money[0]=nums[0];
        if(nums.size()>1) money[1]=(nums[1]>nums[0])?nums[1]:nums[0];
        for(int i=2;i<nums.size();i++)
        {
            money[i]=(money[i-1]>money[i-2]+nums[i])?money[i-1]:money[i-2]+nums[i];
        }
        return money.back();
    }
};
```