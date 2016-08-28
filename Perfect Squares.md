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
        vector<int> squares;
        vector<bool> visited(n);
        for(int i=1;i*i<=n;i++)//get square nums
        {
            squares.push_back(i*i);
        }
        if(squares.back()==n) return 1;//check if n is square num
        
        //BFS
        queue<int> numQueue;
        for(int currentSquare:squares)
        {
            numQueue.push(currentSquare);
            visited[currentSquare-1]=1;
        }
        int numSquare=1;
        while(!numQueue.empty())
        {
            numSquare++;
            int queueSize=numQueue.size();
            for(int i=0;i<queueSize;i++)
            {
                int frontElem=numQueue.front();
                for(int currentSquare:squares)
                {
                    int nextElem=frontElem+currentSquare;
                    if(nextElem==n) return numSquare;
                    else if(nextElem<n&&visited[nextElem-1]==0){
                        visited[nextElem-1]=1;
                        numQueue.push(nextElem);
                    }
                    else if(nextElem>n) break;
                }
                numQueue.pop();
            }
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