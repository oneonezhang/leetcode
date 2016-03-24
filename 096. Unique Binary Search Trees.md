#Unique Binary Search Trees
##Problem:
Given n, how many structurally unique BST's (binary search trees) that store values 1...n?

For example,
Given n = 3, there are a total of 5 unique BST's.
```
   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```
##Idea:
`Dynamic Programming`
```cpp
class Solution {
public:
    int numTrees(int n) {
        int sub[n+1]={0};
        sub[0]=1;
        sub[1]=1;
        for(int i=2;i<=n;i++)
        {
            for(int j=1;j<=i;j++)
            {
                sub[i] += sub[j-1]*sub[i-j];
            }
        }
        return sub[n];
    }
};
```