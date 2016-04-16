#Combination Sum
##Problem:
Given a set of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

The same repeated number may be chosen from C unlimited number of times.

Note:  
All numbers (including target) will be positive integers.  
Elements in a combination (a1, a2, … , ak) must be in non-descending order. (ie, a1 ≤ a2 ≤ … ≤ ak).  
The solution set must not contain duplicate combinations.  
For example, given candidate set 2,3,6,7 and target 7,   
A solution set is:   
[7]   
[2, 2, 3]   
##Idea:
`sort + backtracking`
```cpp
class Solution {
public:
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<vector<int>> result;
        vector<int> current;
        sort(candidates.begin(),candidates.end());
        helper(result,current,candidates,0,0,target);
        return result;
    }
private:
    void helper(vector<vector<int>>& result,vector<int>& current,vector<int>& candidates,int sum,int begin,int target)
    {
        if(sum==target)
        {
            result.push_back(current);
        }
        else
        {
            for(int i=begin;i<candidates.size();i++)
            {
                if(sum+candidates[i]>target)
                {
                    break;
                }
                else
                {
                    current.push_back(candidates[i]);
                    helper(result,current,candidates,sum+candidates[i],i,target);
                    current.pop_back();
                }
            }
        }
    }
};
```
##To Study:
可以将target-candidates[i]作为递归时target的实参，省去sum变量