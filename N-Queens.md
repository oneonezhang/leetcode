#N-Queens
##Problem:
The n-queens puzzle is the problem of placing n queens on an n×n chessboard such that no two queens attack each other.  
Given an integer n, return all distinct solutions to the n-queens puzzle.

Each solution contains a distinct board configuration of the n-queens' placement, where 'Q' and '.' both indicate a queen and an empty space respectively.

For example,
There exist two distinct solutions to the 4-queens puzzle:
```
[
 [".Q..",  // Solution 1
  "...Q",
  "Q...",
  "..Q."],

 ["..Q.",  // Solution 2
  "Q...",
  "...Q",
  ".Q.."]
]
```
##Idea:
在II的基础上对total++部分的代码稍作修改
```cpp
class Solution {
public:
    vector<vector<string>> solveNQueens(int n)
    {
        vector<vector<string>> solutions;
        vector<int> location(n);
        backtrack(0,n,solutions,location);
        return solutions;
    }
private:
    void backtrack(int line,int numQ,vector<vector<string>> &solutions,vector<int> &location)
    {
        if(line>=numQ)
        {
            vector<string> oneSolution;
            for(int i=0;i<numQ;i++)
            {
                string oneLine=""; 
                for(int j=0;j<numQ;j++)
                {
                    oneLine += ".";
                }
                oneLine[location[i]]='Q';
                oneSolution.push_back(oneLine);
            }
            solutions.push_back(oneSolution);
        }
        else
        {
            for(int i=0;i<numQ;i++)
            {
                if(valid(line,i,location)) 
                {
                    location[line]=i;
                    backtrack(line+1,numQ,solutions,location);
                }
            }
        }
    }
    bool valid(int line,int i,vector<int> &location)
    {
        for(int above=0;above<line;above++)
        {
            if(line-above==abs(location[above]-i)||i==location[above]) return 0;
        }
        return 1;
    }
};
```
##To Study:
可以在搜索的时候动态地设置'Q''.'及push_back pop_back（位运算和迭代也同理）
```cpp
class Solution {
public:
    vector<vector<string>> solveNQueens(int n)
    {
        vector<vector<string>> solutions;
        vector<int> location(n);
        vector<string> oneSolution;
        backtrack(0,n,solutions,oneSolution,location);
        return solutions;
    }
private:
    void backtrack(int line,int numQ,vector<vector<string>> &solutions,vector<string> &oneSolution,vector<int> &location)
    {
        if(line>=numQ)
        {
            solutions.push_back(oneSolution);
        }
        else
        {
            for(int i=0;i<numQ;i++)
            {
                if(valid(line,i,location)) 
                {
                    location[line]=i;
                    string oneLine(numQ,'.');
                    oneLine[i]='Q';
                    oneSolution.push_back(oneLine);
                    backtrack(line+1,numQ,solutions,oneSolution,location);
                    oneSolution.pop_back();
                }
            }
        }
    }
    bool valid(int line,int i,vector<int> &location)
    {
        for(int above=0;above<line;above++)
        {
            if(line-above==abs(location[above]-i)||i==location[above]) return 0;
        }
        return 1;
    }
};
```
