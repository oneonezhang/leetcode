#Combinations
##Problem:
Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

For example,
If n = 4 and k = 2, a solution is:
```
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```
##Idea:
`Backtracking`
```cpp
class Solution {
public:
    vector<vector<int>> combine(int n, int k) {
        vector<vector<int>> result;
        vector<int> current;
        helper(result,current,1,n,k);
        return result;
    }
private:
    void helper(vector<vector<int>>& result,vector<int>& current,int begin,int n,int rest)
    {
        if(rest==0) result.push_back(current);
        else if(rest>0)
        {
            for(int i=begin;i<=n;i++)
            {
                current.push_back(i);
                helper(result,current,i+1,n,rest-1);
                current.pop_back();
            }
        }
    }
};
```
##To Study:
optimize:
```cpp
class Solution {
public:
    vector<vector<int>> combine(int n, int k) {
        vector<vector<int>> result;
        vector<int> current(k);
        helper(result,current,1,n,k);
        return result;
    }
private:
    void helper(vector<vector<int>>& result,vector<int>& current,int begin,int n,int rest)
    {
        if(rest==0) result.push_back(current);
        else if(rest>0)
        {
            for(int i=begin;i<=n-rest+1;i++)
            {
                current[current.size()-rest]=i;
                helper(result,current,i+1,n,rest-1);
            }
        }
    }
};
```