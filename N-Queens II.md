#N-Queens II
##Problem:
Follow up for N-Queens problem.

Now, instead outputting board configurations, return the total number of distinct solutions.
##Idea:
`recursion`
```cpp
class Solution {
public:
    int totalNQueens(int n)
    {
        int total=0;
        vector<int> location(n);
        backtrack(0,n,total,location);
        return total;
    }
private:
    void backtrack(int line,int numQ,int &total,vector<int> &location)
    {
        if(line>=numQ)
        {
            total++;
        }
        else
        {
            for(int i=0;i<numQ;i++)
            {
                if(valid(line,i,location)) 
                {
                    location[line]=i;
                    backtrack(line+1,numQ,total,location);
                }
            }
        }
    }
    bool valid(int line,int i,vector<int> &location)
    {
        for(int above=0;above<line;above++)
        {
            if(line-above==abs(location[above]-i)||i==location[above]) return 0;
        }
        return 1;
    }
};
```
##To Study:
1.可以用bool[n]来记录列是否被占用，bool[2*n-1]记录对角线是否被占用  
2.`bitwise operation`+`recursion`
```cpp
class Solution {
public:
    int totalNQueens(int n) {
        int total=0;
        nQueen(n,0,0,0,total);
        return total;
    }
private:
    void nQueen(int n,int column,int leftDown,int rightDown,int &total)
    {
        if(column==((1<<n)-1))
        {
            total++;
        }
        else
        {
            int choice=~(column|leftDown|rightDown)&((1<<n)-1);
            while(choice)
            {
                int pos=choice&(-choice);
                choice -= pos;
                nQueen(n,column+pos,(leftDown+pos)<<1,(rightDown+pos)>>1,total);
            }
        }
    }
};
```
3.`iteration`
```cpp
class Solution {
public:
    int totalNQueens(int n) {
        int total=0;
        int board[n];
        int row=0;
        memset(board,-1,n*sizeof(int));
        while(row!=-1)
        {
            if(row==n)
            {
                total++;
                row--;
            }
            int i=board[row]+1;
            for(;i<n;i++)
            {
                if(valid(row,i,board)) 
                {
                    board[row]=i;
                    row++;
                    break;
                }
            }
            if(i==n)
            {
                board[row]=-1;
                row--;
            }
        }
        return total;
    }
private:
    bool valid(int line,int i,int board[])
    {
        for(int above=0;above<line;above++)
        {
            if(line-above==abs(i-board[above])||i==board[above]) return 0;
        }
        return 1;
    }
};
```
