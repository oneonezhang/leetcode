#Combination Sum II
##Problem:
Given a collection of candidate numbers (C) and a target number (T), find all unique combinations in C where the candidate numbers sums to T.

Each number in C may only be used once in the combination.

Note:  
All numbers (including target) will be positive integers.  
Elements in a combination (a1, a2, … , ak) must be in non-descending order. (ie, a1 ≤ a2 ≤ … ≤ ak).  
The solution set must not contain duplicate combinations.  
For example, given candidate set 10,1,2,7,6,1,5 and target 8,   
A solution set is:   
[1, 7]   
[1, 2, 5]   
[2, 6]   
[1, 1, 6]  
##Idea:
1.check if the current combination exists before adding//19ms
```cpp
class Solution {
public:
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        vector<vector<int>> result;
        vector<int> current;
        sort(candidates.begin(),candidates.end());
        helper(result,current,candidates,0,target);
        return result;
    }
private:
    void helper(vector<vector<int>>& result,vector<int>& current,vector<int>& candidates,int begin,int target)
    {
        if(target==0)
        {
            if(find(result.begin(),result.end(),current)==result.end()) 
            {
                result.push_back(current);
            }
        }
        else
        {
            for(int i=begin;i<candidates.size();i++)
            {
                if(candidates[i]>target)
                {
                    break;
                }
                else
                {
                    current.push_back(candidates[i]);
                    helper(result,current,candidates,i+1,target-candidates[i]);
                    current.pop_back();
                }
            }
        }
    }
};
```
2.In the for-loop, if candidates[i]==candidates[i-1], then we can skip candidates[i] since candidates[i-1] can generate the same combinations//8ms
```cpp
class Solution {
public:
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        vector<vector<int>> result;
        vector<int> current;
        sort(candidates.begin(),candidates.end());
        helper(result,current,candidates,0,target);
        return result;
    }
private:
    void helper(vector<vector<int>>& result,vector<int>& current,vector<int>& candidates,int begin,int target)
    {
        if(target==0)
        {
            result.push_back(current);
        }
        else
        {
            for(int i=begin;i<candidates.size();i++)
            {
                if(candidates[i]>target)
                {
                    break;
                }
                else if(i>begin&&candidates[i]==candidates[i-1])
                {
                    continue;
                }
                else
                {
                    current.push_back(candidates[i]);
                    helper(result,current,candidates,i+1,target-candidates[i]);
                    current.pop_back();
                }
            }
        }
    }
};
```
PS:
Collection:无序，可以有重复  
List:有序  
Set:不能有重复