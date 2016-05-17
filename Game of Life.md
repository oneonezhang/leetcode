#Game of Life
##Problem:
According to the Wikipedia's article: "The Game of Life, also known simply as Life, is a cellular automaton devised by the British mathematician John Horton Conway in 1970."

Given a board with m by n cells, each cell has an initial state live (1) or dead (0). Each cell interacts with its eight neighbors (horizontal, vertical, diagonal) using the following four rules (taken from the above Wikipedia article):

1. Any live cell with fewer than two live neighbors dies, as if caused by under-population.  
2. Any live cell with two or three live neighbors lives on to the next generation.  
3. Any live cell with more than three live neighbors dies, as if by over-population.  
4. Any dead cell with exactly three live neighbors becomes a live cell, as if by reproduction.  
Write a function to compute the next state (after one update) of the board given its current state.

Follow up: 
1. Could you solve it in-place? Remember that the board needs to be updated at the same time: You cannot update some cells first and then use their updated values to update other cells.  
2. In this question, we represent the board using a 2D array. In principle, the board is infinite, which would cause problems when the active area encroaches the border of the array. How would you address these problems?  
  
##Idea:
use a vector to record the elements which need to be changed
```cpp
class Solution {
public:
    void gameOfLife(vector<vector<int>>& board) {
        int m=board.size();
        if(m==0) return;
        int n=board[0].size();
        if(n==0) return;
        vector<int> change;
        for(int i=0;i<m*n;i++)
        {
            if(searchArea(i,board)) change.push_back(i);
        }
        for(int elem:change)
        {
            board[elem/n][elem%n]=1-board[elem/n][elem%n];
        }
    }
private:
    bool searchArea(int current,vector<vector<int>>& board)
    {
        int m=board.size(),n=board[0].size();
        int i=current/n,j=current%n;
        int left=max(0,j-1),right=min(n-1,j+1);
        int up=max(0,i-1),down=min(m-1,i+1);
        int count=0;
        for(int row=up;row<=down;row++)
        {
            for(int col=left;col<=right;col++)
            {
                if(board[row][col]) count++;
            }
        }
        count -= board[i][j];
        if(board[i][j]&&(count>3||count<2)) return true;
        else if(!board[i][j]&&count==3) return true;
        else return false;
    }
};
```
**This may not be in-place->(only use a constant amount of variables, no auxiliary data structure)**
##To Study:
use 2 bits to record the next state and the current state   
board[i][j]&1->current state  
board[i][j]>>=1->update
```cpp
class Solution {
public:
    void gameOfLife(vector<vector<int>>& board) {
        if(board.empty()||board[0].empty()) return;
        int m=board.size(),n=board[0].size();
        for(int i=0;i<m;i++)
            for(int j=0;j<n;j++)
            {
                int count=-board[i][j];
                for(int row=max(0,i-1);row<=min(m-1,i+1);row++)
                    for(int col=max(0,j-1);col<=min(n-1,j+1);col++)
                        if(board[row][col]&1) count++;
                if(board[i][j]&&count>=2&&count<=3) board[i][j] += 2;
                else if(!board[i][j]&&count==3) board[i][j] += 2;
            }
        for(int i=0;i<m;i++)
            for(int j=0;j<n;j++)
                board[i][j] >>= 1;
    }
};
```