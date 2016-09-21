#Subsets
##Problem:
Given a set of distinct integers, nums, return all possible subsets.

Note: The solution set must not contain duplicate subsets.

For example,
If nums = [1,2,3], a solution is:
```
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```
##Idea:
`Backtracking`
```cpp
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> result;
        vector<int> current;
        result.push_back(current);
        backTrack(0,current,nums,result);
        return result;
    }
private:
    void backTrack(int start, vector<int>& current, vector<int>& nums, vector<vector<int>>& result)
    {
        for(int i=start;i<nums.size();i++)
        {
            current.push_back(nums[i]);
            result.push_back(current);
            backTrack(i+1,current,nums,result);
            current.pop_back();
        }
    }
};
```
##To Study:
1.`Iteration`
```cpp
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> result(1,vector<int>());
        for(int i=0;i<nums.size();i++)
        {
            int n=result.size();
            for(int j=0;j<n;j++)
            {
                result.push_back(result[j]);
                result.back().push_back(nums[i]);
            }
        }
        return result;
    }
};
```
2.`Bit Manipulation`
```cpp
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        int n=nums.size();
        int subsetNum=pow(2,n);
        vector<vector<int>> result(subsetNum,vector<int>());
        for(int i=0;i<n;i++)
        {
            for(int j=0;j<subsetNum;j++)
            {
                if(j>>i&1)
                {
                    result[j].push_back(nums[i]);
                }
            }
        }
        return result;
    }
};
```