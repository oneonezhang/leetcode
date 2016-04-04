#Generate Parentheses
##Problem:
Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:

"((()))", "(()())", "(())()", "()(())", "()()()"
##Idea:
`backtracking`
```cpp
class Solution {
public:
    vector<string> generateParenthesis(int n) {
        vector<string> parenthesis;
        helper(parenthesis,0,0,n,"");
        return parenthesis;
    }
private:
    void helper(vector<string>& parenthesis,int left,int right,int n,string current)
    {
        if(left==n&&right==n)
        {
            parenthesis.push_back(current);
        }
        else
        {
            if(left<n)
            {
                helper(parenthesis,left+1,right,n,current+'(');
            }
            if(right<left)
            {
                helper(parenthesis,left,right+1,n,current+')');
            }
        }
    }
};
```
