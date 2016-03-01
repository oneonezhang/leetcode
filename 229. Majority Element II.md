#Majority Element II
##Problem:
Given an integer array of size n, find all elements that appear more than ⌊ n/3 ⌋ times. The algorithm should run in linear time and in O(1) space.
##Idea:
1.Hash Table  
2.Moore Voting Algorithm   
`At most two elements appear more than ⌊ n/3 ⌋ times`  
本来想定义candidates和counts两个vector，count减为0了从vector中删除  
可是如果同时要删的话下标就不对了出现Runtime Error
```cpp
class Solution {
public:
    vector<int> majorityElement(vector<int>& nums) {
        vector<int> candidates;
        int candidate1,candidate2;
        int count1=0,count2=0;
        for(int i=0;i<nums.size();i++)
        {
            if(count1==0&&(count2==0||nums[i]!=candidate2))
            {
                candidate1=nums[i];
                count1++;
            }
            else if(count2==0&&nums[i]!=candidate1)
            {
                candidate2=nums[i];
                count2++;
            }
            else if(nums[i]==candidate1)
            {
                count1++;
            }
            else if(nums[i]==candidate2)
            {
                count2++;
            }
            else
            {
                count1--;
                count2--;
            }
        }
        if(count1!=0&&count(nums.begin(),nums.end(),candidate1)>nums.size()/3) candidates.push_back(candidate1);
        if(count2!=0&&count(nums.begin(),nums.end(),candidate2)>nums.size()/3) candidates.push_back(candidate2);  
        return candidates;
    }
};
```  
**注意最后的count1，count2非零一定要判断，不然会出现candidate2没有被赋值使用上一个test case中的导致Wrong Answer的情况。提交了32次后终于发现了T T**
##To Study:
可以对candidate1和candidate2赋初值解决上面的Wrong Answer问题。  
for循环中条件选择先判断是否相等再判断count是否为0的逻辑更清楚。