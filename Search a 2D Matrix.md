#Search a 2D Matrix
##Problem:
Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

Integers in each row are sorted from left to right.
The first integer of each row is greater than the last integer of the previous row.
For example,

Consider the following matrix:
```
[
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
```
Given target = 3, return true.
##Idea:
`Binary Search`
```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        if(matrix.empty()||matrix[0].empty()||target<matrix[0][0])
        {
            return false;
        }
        
        //search the row
        int up=0,down=matrix.size();
        while(down-up>1)
        {
            int middleRow=(down+up)/2;
            if(target<matrix[middleRow][0]) 
            {
                down=middleRow;
            }
            else
            {
                up=middleRow;
            }
        }
        
        //search the column
        int left=0,right=matrix[up].size()-1;
        while(left<=right)
        {
            int middleCol=(left+right)/2;
            if(target==matrix[up][middleCol]) return true;
            else if(target<matrix[up][middleCol]) right=middleCol-1;
            else left=middleCol+1;
        }
        return false;
    }
};
```
##To Study:
regard the matrix as an 1D array——length m*n
```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        if(matrix.empty()||matrix[0].empty()) return false;
        int m=matrix.size();
        int n=matrix[0].size();
        int left=0,right=m*n-1;
        while(left<=right)
        {
            int middle=(left+right)/2;
            if(target==matrix[middle/n][middle%n]) return true;
            else if(target<matrix[middle/n][middle%n]) right=middle-1;
            else left=middle+1;
        }
        return false;
    }
};
```