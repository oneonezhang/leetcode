#Combination Sum III
##Problem:
Find all possible combinations of k numbers that add up to a number n, given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.

Ensure that numbers within the set are sorted in ascending order.


Example 1:

Input: k = 3, n = 7

Output:

[[1,2,4]]

Example 2:

Input: k = 3, n = 9

Output:

[[1,2,6], [1,3,5], [2,3,4]]
##Idea:
`Backtracking`
```cpp
class Solution {
public:
    vector<vector<int>> combinationSum3(int k, int n) {
        vector<vector<int>> result;
        vector<int> current;
        if(n<=45) helper(result,current,1,k,n);
        return result;
    }
private:
    void helper(vector<vector<int>>& result,vector<int>& current,int begin,int restNum,int target)
    {
        if(restNum==0&&target==0)
        {
            result.push_back(current);
        }
        else if(restNum>0)
        {
            for(int i=begin;i<=9;i++)
            {
                if(i>target) break;
                else
                {
                    current.push_back(i);
                    helper(result,current,i+1,restNum-1,target-i);
                    current.pop_back();
                }
            }
        }
    }
};
```