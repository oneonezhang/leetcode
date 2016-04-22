#Spiral Matrix II
##Problem:
Given an integer n, generate a square matrix filled with elements from 1 to n2 in spiral order.

For example,
Given n = 3,

You should return the following matrix:
```
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]
```
##Idea:
1.judge if the next one goes beyond the area or has been filled
```cpp
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>> matrix(n,vector<int>(n,0));
        int current=1;
        int direction=1;
        int i=0,j=0;
        while(current<=n*n)
        {
            matrix[i][j]=current;
            current++;
            switch(direction)
            {
                case 1:if(j+1>=n||matrix[i][j+1]!=0)
                {
                    direction=2;i++;
                }
                else j++;
                break;
                case 2:if(i+1>=n||matrix[i+1][j]!=0)
                {
                    direction=3;j--;
                }
                else i++;
                break;
                case 3:if(j-1<0||matrix[i][j-1]!=0)
                {
                    direction=4;i--;
                }
                else j--;
                break;
                case 4:if(i-1<0||matrix[i-1][j]!=0)
                {
                    direction=1;j++;
                }
                else i--;
                break;                
            }
        }
        return matrix;
    }
};
```
2.use 4 variables to record
```cpp
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>> matrix(n,vector<int>(n,0));
        int rowMin=0;
        int rowMax=n-1;
        int colMin=0;
        int colMax=n-1;
        int current=1;
        while(true)
        {
            for(int j=colMin;j<=colMax;j++)
            {
                matrix[rowMin][j]=current;current++;
            }
            rowMin++;
            if(rowMin>rowMax) break;
            for(int i=rowMin;i<=rowMax;i++)
            {
                matrix[i][colMax]=current;current++;
            }
            colMax--;
            if(colMin>colMax) break;
            for(int j=colMax;j>=colMin;j--)
            {
                matrix[rowMax][j]=current;current++;
            }
            rowMax--;
            if(rowMin>rowMax) break;
            for(int i=rowMax;i>=rowMin;i--)
            {
                matrix[i][colMin]=current;current++;
            }
            colMin++;
            if(colMin>colMax) break;
        }
        return matrix;
    }
};
```
3.use an array of direction offsets
```cpp
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>> matrix(n,vector<int>(n,0));
        vector<vector<int>> direction={{0,1},{1,0},{0,-1},{-1,0}};
        int position[2]={0,-1};
        int current=1;
        int d=0;
        int row=n-1,col=n;
        while(current<=n*n)
        {
            for(int i=0;i<col;i++)
            {
                position[0] += direction[d][0];
                position[1] += direction[d][1];
                matrix[position[0]][position[1]]=current;
                current++;
            }
            col--;
            swap(col,row);
            d=(d+1)%4;
        }
        return matrix;
    }
};
```