#Set Matrix Zeroes
##Problem:
Given a m x n matrix, if an element is 0, set its entire row and column to 0. Do it in place.  
Follow up:  
Did you use extra space?  
A straight forward solution using O(mn) space is probably a bad idea.  
A simple improvement uses O(m + n) space, but still not the best solution.  
Could you devise a constant space solution?  
##Idea:
assign matrix[i][0] or matrix[0][j] =0 to indicate that row i or col j should be set to 0.
```cpp
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        if(matrix.empty()||matrix[0].empty()) return;
        int m=matrix.size();
        int n=matrix[0].size();
        bool row=1,col=1;//The meaning of matrix[0][0]==0:row==0->row0,col==0->col0
        for(int i=0;i<m;i++)
        {
            for(int j=0;j<n;j++)
            {
                if(matrix[i][j]==0)
                {
                    matrix[0][j]=0;
                    matrix[i][0]=0;
                    if(i==0) row=0;
                    if(j==0) col=0;
                }
            }
        }
        for(int i=1;i<m;i++)
        {
            for(int j=1;j<n;j++)
            {
                if(matrix[i][0]==0||matrix[0][j]==0)
                    matrix[i][j]=0;
            }
        }
        if(col==0)
        {
            for(int i=1;i<m;i++) matrix[i][0]=0;
        }
        if(row==0)
        {
            for(int j=1;j<n;j++) matrix[0][j]=0;
        }
        
    }
};
```
**Pay attention to matrix[0][0]**
##To Study:
we can use matrix[0][0] to represent row 0, and use another variable col0 to represent col 0.
```cpp
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        if(matrix.empty()||matrix[0].empty()) return;
        int m=matrix.size();
        int n=matrix[0].size();
        bool col0=1;
        for(int i=0;i<m;i++)
        {
            if(matrix[i][0]==0) col0=0;
            for(int j=1;j<n;j++)
            {
                if(matrix[i][j]==0)
                {
                    matrix[0][j]=0;
                    matrix[i][0]=0;
                }
            }
        }
        for(int i=m-1;i>=0;i--)
        {
            for(int j=n-1;j>=1;j--)
            {
                if(matrix[i][0]==0||matrix[0][j]==0)
                    matrix[i][j]=0;  
            }
            if(col0==0) matrix[i][0]=0;
        }
    }
};
```