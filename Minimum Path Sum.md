#Minimum Path Sum
##Problem:
Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.
##Idea:
`Dynamic Programming`
```cpp
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        if(grid.empty()) return 0;
        int m=grid.size();
        int n=grid[0].size();
        if(n==0) return 0;
        int stepHereSum[n];
        stepHereSum[0]=grid[0][0];
        for(int i=1;i<n;i++)
        {
            stepHereSum[i] = stepHereSum[i-1] + grid[0][i];
        }
        for(int j=1;j<m;j++)
        {
            stepHereSum[0] += grid[j][0];
            for(int i=1;i<n;i++)
            {
                stepHereSum[i] =min(stepHereSum[i],stepHereSum[i-1])+grid[j][i];
            }
        }
        return stepHereSum[n-1];
    }
};
```