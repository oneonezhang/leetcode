#Perfect Squares
##Problem:
Given a positive integer n, find the least number of perfect square numbers (for example, 1, 4, 9, 16, ...) which sum to n.

For example, given n = 12, return 3 because 12 = 4 + 4 + 4; given n = 13, return 2 because 13 = 4 + 9.
##Idea:
`Dynamic Programming`——O(n^1.5)
```cpp
class Solution {
public:
    int numSquares(int n) {
        int record[n+1];
        int nextSquare=1;
        for(int i=1;i<=n;i++)
        {
            if(i==nextSquare*nextSquare)
            {
                record[i]=1;
                nextSquare++;
            }
            else
            {
                record[i]=i;
                for(int j=nextSquare-1;j>=1;j--)
                {
                    record[i]=min(record[i],record[i-j*j]+1);
                }
            }
        }
        return record[n];
    }
};
```
##To Study:
1.BFS
```cpp
class Solution {
public:
    int numSquares(int n) {
        queue<int> numQueue;
        vector<bool> visited(n);
        numQueue.push(0);
        int numOfSquare=1;;
        while(!numQueue.empty())
        {
            int length=numQueue.size();
            for(int i=0;i<length;i++)
            {
                int current=numQueue.front();
                numQueue.pop();
                for(int root=1;root*root<=n;root++)
                {
                    int next=current+root*root;
                    if(next==n) {
                        return numOfSquare;
                    }
                    else if(next<n&&visited[next-1]==0) {
                        numQueue.push(next);
                        visited[next-1]=1;
                    }
                    else if(next>n) break;
                }
            }
            numOfSquare++;
        }
        return 0;
    }
};
```
2.Math  
Lagrange's Four Squares Theorem  
The result is 4 if and only if n=4^k(8*m+7)
```cpp
class Solution {
public:
    int numSquares(int n) {
        if(isSquare(n)) return 1;
        for(int i=1;i*i<=n;i++)
        {
            if(isSquare(n-i*i)) return 2;
        }
        while(n%4==0) n/=4;
        if(n%8==7) return 4;
        return 3;
    }
private:
    bool isSquare(int n)
    {
        int sqrtNum=sqrt(n);
        return (n==sqrtNum*sqrtNum);
    }
};
```