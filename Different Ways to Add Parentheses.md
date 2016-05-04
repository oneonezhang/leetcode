#Different Ways to Add Parentheses
##Problem:
Given a string of numbers and operators, return all possible results from computing all the different possible ways to group numbers and operators. The valid operators are +, - and *.


Example 1  
Input: "2-1-1".  

((2-1)-1) = 0  
(2-(1-1)) = 2  
Output: [0, 2]  


Example 2  
Input: "2*3-4*5"  

(2*(3-(4*5))) = -34  
((2*3)-(4*5)) = -14  
((2*(3-4))*5) = -10  
(2*((3-4)*5)) = -10  
(((2*3)-4)*5) = 10  
Output: [-34, -14, -10, -10, 10]
##Idea:
`Dynamic Programmnig`——learn from Problem `Unique Binary Search Trees` and `Burst Balloons`
```cpp
class Solution {
public:
    vector<int> diffWaysToCompute(string input) {
        vector<int> result;
        if(input=="") return result;
        vector<int> nums;
        vector<char> signs;
        
        int begin=0;
        for(int i=0;i<input.size();i++)
        {
            if(input[i]=='+'||input[i]=='-'||input[i]=='*')
            {
                //can deal with cases like "-1" because atoi("")=0 and we add 0 at the beginning of nums
                nums.push_back(atoi(input.substr(begin,i-begin).c_str()));
                signs.push_back(input[i]);
                begin=i+1;
            }
        }
        nums.push_back(atoi(input.substr(begin).c_str()));
        
        //dynamic programming
        int n=nums.size();
        vector<vector<vector<int>>> dp(n,vector<vector<int>>(n));
        for(int d=0;d<n;d++)
        {
            for(int s=0;s<n-d;s++)
            {
                int e=d+s;
                if(e==s) dp[s][e].push_back(nums[s]);
                else
                for(int m=s;m<e;m++)
                {
                    for(int i:dp[s][m])
                    {
                        for(int j:dp[m+1][e])
                        {
                            if(signs[m]=='+') dp[s][e].push_back(i+j);
                            else if(signs[m]=='-') dp[s][e].push_back(i-j);
                            else dp[s][e].push_back(i*j);
                        }
                    }
                }
            }
        }
        return dp[0][n-1];
    }
};
```
##To Study:
`Divide and Conquer with memoization`
```cpp
class Solution {
public:
    vector<int> diffWaysToCompute(string input) {
        unordered_map<string,vector<int>> record;
        return divideAndConquer(input,record);
    }
private:
    vector<int> divideAndConquer(string input,unordered_map<string,vector<int>>& record)
    {
        if(record.find(input)!=record.end()) return record[input];
        else
        {
            vector<int> result;
            for(int i=0;i<input.size();i++)
            {
                if(input[i]=='+'||input[i]=='-'||input[i]=='*')
                {
                    vector<int> left=divideAndConquer(input.substr(0,i),record);
                    vector<int> right=divideAndConquer(input.substr(i+1),record);
                    for(int l:left)
                    {
                        for(int r:right)
                        {
                            if(input[i]=='+') result.push_back(l+r);
                            else if(input[i]=='-') result.push_back(l-r);
                            else result.push_back(l*r);
                        }
                    }
                }
            }
            if(result.empty()) result.push_back(atoi(input.c_str()));
            record[input]=result;
            return result;
        }
    }
};
```