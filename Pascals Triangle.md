#Pascal's Triangle
##Problem:
Given numRows, generate the first numRows of Pascal's triangle.

For example, given numRows = 5,
Return
```
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```
##Idea:
```cpp
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> result;
        if(numRows<1) return result;
        result.push_back(vector<int>(1,1));
        for(int i=1;i<numRows;i++)
        {
            vector<int> newLine(i+1);
            newLine[0]=result[i-1][0];
            for(int j=1;j<i;j++)
            {
                newLine[j]=result[i-1][j-1]+result[i-1][j];
            }
            newLine[i]=result[i-1][i-1];
            result.push_back(newLine);
        }
        return result;
    }
};
```
##To Study:
use resize and do it in-place.
```cpp
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> result(numRows);
        for(int i=0;i<numRows;i++)
        {
            result[i].resize(i+1);
            result[i][0]=1;
            for(int j=1;j<i;j++)
            {
                result[i][j]=result[i-1][j-1]+result[i-1][j];
            }
            result[i][i]=1;
        }
        return result;
    }
};
```
