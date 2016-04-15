#Permutations
##Problem:
Given a collection of distinct numbers, return all possible permutations.

For example,  
[1,2,3] have the following permutations:  
[1,2,3], [1,3,2], [2,1,3], [2,3,1], [3,1,2], and [3,2,1].
##Idea:
`Backtracking`
```cpp
class Solution {
public:
    vector<vector<int>> permute(vector<int>& nums) {
        vector<bool> used(nums.size());
        vector<int> current;
        vector<vector<int>> result;
        helper(result,current,nums,used);
        return result;
    }
private:
    void helper(vector<vector<int>>& result,vector<int>& current,vector<int>& nums,vector<bool>& used)
    {
        if(current.size()==nums.size()) result.push_back(current);
        else 
        {
            for(int i=0;i<nums.size();i++)
            {
                if(used[i]==0)
                {
                    used[i]=1;
                    current.push_back(nums[i]);
                    helper(result,current,nums,used);
                    used[i]=0;
                    current.pop_back();
                }
            }
        }
    }
};
```
##To Study:
Use `swap`
```cpp
class Solution {
public:
    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> result;
        helper(nums,result,0);
        return result;
    }
private:
    void helper(vector<int>& nums,vector<vector<int>>& result,int begin)
    {
        if(begin==nums.size()) result.push_back(nums);
        else
        {
            for(int i=begin;i<nums.size();i++)
            {
                swap(nums[begin],nums[i]);
                helper(nums,result,begin+1);
                swap(nums[begin],nums[i]);
            }
        }
    }
};
```