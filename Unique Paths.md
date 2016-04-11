#Unique Paths
##Problem:
A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?


Above is a 3 x 7 grid. How many possible unique paths are there?

Note: m and n will be at most 100.
##Idea:
`Dynamic Programming`
```cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        int sub[m][n];
        for(int i=0;i<m;i++)
        {
            for(int j=0;j<n;j++)
            {
                if(i==0||j==0) sub[i][j]=1;
                else sub[i][j] = sub[i][j-1]+sub[i-1][j];
            }
        }
        return sub[m-1][n-1];
    }
};
//Space Complexity:O(m*n)
```
##To Study:
1.1-D array
```cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        if(m>n) return uniquePaths(n,m);
        vector<int> current(m,1);
        for(int j=1;j<n;j++)
        {
            for(int i=1;i<m;i++)
            {
                current[i] += current[i-1];
            }
        }
        return current[m-1];
    }
};
//Space Complexity:O(min(m,n))
```
2.Math C(m+n-2,m-1)
```cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        long result=1;
        for(int i=1;i<=m-1;i++)
        {
            result = result*(i+n-1)/i;
        }
        return (int)result;
    }
};
```
**注意要转换为long，不然可能超出范围出错**

