#Search a 2D Matrix II
##Problem:
Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

Integers in each row are sorted in ascending from left to right.  
Integers in each column are sorted in ascending from top to bottom.  
For example,

Consider the following matrix:  
```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```
Given target = 5, return true.

Given target = 20, return false.
##Idea:
`Divide and Conquer` //my method is very slow >.< T(mxn)=3T(mxn/4)
```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        if(matrix.empty()||matrix[0].empty()) return false;
        int left=0,right=matrix[0].size()-1,up=0,down=matrix.size()-1;
        return helper(matrix,left,right,up,down,target);
    }
private:
    bool helper(vector<vector<int>>& matrix,int left,int right,int up,int down,int target)
    {
        if(right-left<=1&&down-up<=1)
        {
            for(int i=up;i<=down;i++)
                for(int j=left;j<=right;j++)
                    if(matrix[i][j]==target) return true;
            return false;
        }
        else
        {
            int midRow=(up+down)/2,midCol=(left+right)/2;
            bool area1,area2,area3;
            if(matrix[midRow][midCol]==target) return true;
            else if(target<matrix[midRow][midCol]) area1=helper(matrix,left,midCol,up,midRow,target);
            else area1=helper(matrix,midCol,right,midRow,down,target);
            if(area1) return true;
            area2=helper(matrix,midCol+1,right,up,midRow-1,target);
            if(area2) return true;
            area3=helper(matrix,left,midCol-1,midRow+1,down,target);
            if(area3) return true;
            return false;
        }
    }
};
```
##To Study:
1.Optimize my method  
`Make the rightdown area be the smallest` //Still need to pay attention to the 1x1 condition  
`If one sub-area returns true, return true immediately`
```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        if(matrix.empty()||matrix[0].empty()) return false;
        int left=0,right=matrix[0].size()-1,up=0,down=matrix.size()-1;
        return helper(matrix,left,right,up,down,target);
    }
private:
    bool helper(vector<vector<int>>& matrix,int left,int right,int up,int down,int target)
    {
        if(right<left||down<up)
            return false;
        else if(right==left&&down==up)
            return matrix[up][left]==target;
        else
        {
            int midRow=(up+down)/2,midCol=(left+right)/2;
            if(matrix[midRow][midCol]==target) 
                return true;
            else if(target<matrix[midRow][midCol]) 
                return helper(matrix,left,midCol,up,midRow,target)||helper(matrix,midCol+1,right,up,midRow,target)||
                        helper(matrix,left,midCol,midRow+1,down,target);
            else 
                return helper(matrix,midCol+1,right,midRow+1,down,target)||helper(matrix,midCol+1,right,up,midRow,target)||
                        helper(matrix,left,midCol,midRow+1,down,target);
        }
    }
};
```
2.`Binary Search` //O(m+n)
```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        if(matrix.empty()||matrix[0].empty()) return false;
        int m=matrix.size(),n=matrix[0].size();
        int row=0,col=n-1;
        while(row<m&&col>=0)
        {
            if(target==matrix[row][col]) return true;
            else if(target<matrix[row][col]) col--;
            else row++;
        }
        return false;
    }
};
```