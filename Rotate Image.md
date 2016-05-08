#Rotate Image
##Problem:
You are given an n x n 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).

Follow up:
Could you do this in-place?
##Idea:
rotate n/2 rings from margin to center
```cpp
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n=matrix.size();
        for(int i=0;i<n/2;i++)
        {
            for(int j=i;j<n-i-1;j++)
            {
                int temp=matrix[i][j];
                matrix[i][j]=matrix[n-1-j][i];
                matrix[n-1-j][i]=matrix[n-1-i][n-1-j];
                matrix[n-1-i][n-1-j]=matrix[j][n-1-i];
                matrix[j][n-1-i]=temp;
            }
        }
    }
};
```
##To Study:
1.We can also rotate one-fourth of the matrix  
2.`flip-flip`
```
 123   ->  147   ->   741    
 456       258        852
 789       369        963
```
```cpp
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        //flip symmetrically
        int n=matrix.size();
        for(int i=0;i<n;i++)
        {
            for(int j=0;j<i;j++)
            {
                swap(matrix[i][j],matrix[j][i]);
            }
        }
        
        //flip horizontally
        for(int i=0;i<n;i++)
        {
            for(int j=0;j<n/2;j++)
            {
                swap(matrix[i][j],matrix[i][n-1-j]);
            }
        }
    }
};
```
