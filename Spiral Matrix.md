#Spiral Matrix
##Problem:
Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

For example,
Given the following matrix:
```
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
```
You should return [1,2,3,6,9,8,7,4,5].
##Idea:
1.use another matrix to record if it has been visited
```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector<int> elements;
        int m=matrix.size();
        if(m!=0)
        {
            int n=matrix[0].size();
            vector<vector<bool>> visited(m,vector<bool>(n,0));
            int direction=1;
            int i=0,j=0;
            while(elements.size()!=m*n)
            {
                elements.push_back(matrix[i][j]);
                visited[i][j]=1;
                switch(direction)
                {
                    case 1: if(j+1>=n||visited[i][j+1]==1) 
                            {
                                i=i+1;direction=2;
                            }
                            else j++;
                            break;
                    case 2: if(i+1>=m||visited[i+1][j]==1)
                            {
                                j=j-1;direction=3;
                            }
                            else i++;
                            break;
                    case 3: if(j-1<0||visited[i][j-1]==1)
                            {
                                i=i-1;direction=4;
                            }
                            else j--;
                            break;
                    case 4: if(i-1<0||visited[i-1][j]==1)
                            {
                                j=j+1;direction=1;
                            }
                            else i--;
                            break;
                }
            }
        }
        return elements;
    }
};
```
2.use 4 variables:upMin,downMax,leftMin,rightMax
```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector<int> elements;
        int m=matrix.size();
        if(m!=0)
        {
            int n=matrix[0].size();
            int rightMax=n-1;
            int downMax=m-1;
            int leftMin=0;
            int upMin=0;
            int i=0,j=-1;
            while(true)
            {
                for(j=j+1;j<=rightMax;j++)
                {
                    elements.push_back(matrix[i][j]);
                }
                j--;
                upMin++;
                if(upMin>downMax) break;
                for(i=i+1;i<=downMax;i++)
                {
                    elements.push_back(matrix[i][j]);
                }
                i--;
                rightMax--;
                if(leftMin>rightMax) break;
                for(j=j-1;j>=leftMin;j--)
                {
                    elements.push_back(matrix[i][j]);
                }
                j++;
                downMax--;
                if(upMin>downMax) break;
                for(i=i-1;i>=upMin;i--)
                {
                    elements.push_back(matrix[i][j]);
                }
                i++;
                leftMin++;
                if(leftMin>rightMax) break;
            }
        }
        return elements;
    }
};
```
##To Study:
1.some improvements
```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector<int> elements;
        int m=matrix.size();
        if(m!=0)
        {
            int n=matrix[0].size();
            int rightMax=n-1;
            int downMax=m-1;
            int leftMin=0;
            int upMin=0;
            while(true)
            {
                for(int j=leftMin;j<=rightMax;j++)
                {
                    elements.push_back(matrix[upMin][j]);
                }
                upMin++;
                if(upMin>downMax) break;
                for(int i=upMin;i<=downMax;i++)
                {
                    elements.push_back(matrix[i][rightMax]);
                }
                rightMax--;
                if(leftMin>rightMax) break;
                for(int j=rightMax;j>=leftMin;j--)
                {
                    elements.push_back(matrix[downMax][j]);
                }
                downMax--;
                if(upMin>downMax) break;
                for(int i=downMax;i>=upMin;i--)
                {
                    elements.push_back(matrix[i][leftMin]);
                }
                leftMin++;
                if(leftMin>rightMax) break;
            }
        }
        return elements;
    }
};
```
2.use an array of direction offsets
```cpp
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        vector<vector<int>> direction={{1,0},{0,-1},{-1,0},{0,1}};
        vector<int> elements;
        int m=matrix.size();
        if(m!=0)
        {
            int n=matrix[0].size();
            elements=matrix[0];
            int rest=m*n-n;
            int position[2]={0,n-1};
            int dirNum=0;
            while(rest>0)
            {
                for(int i=1;i<m;i++)
                {
                    position[0] += direction[dirNum][0];
                    position[1] += direction[dirNum][1]; 
                    elements.push_back(matrix[position[0]][position[1]]);
                    rest--;
                }
                m--;
                swap(m,n);
                dirNum=(dirNum+1)%4;
            }
        }
        return elements;
    }
};
```