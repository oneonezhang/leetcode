# Nim Game  
## Problem:  
You are playing the following Nim Game with your friend: There is a heap of stones on the table, each time one of you take turns to remove 1 to 3 stones. The one who removes the last stone will be the winner. You will take the first turn to remove the stones.

Both of you are very clever and have optimal strategies for the game. Write a function to determine whether you can win the game given the number of stones in the heap.

For example, if there are 4 stones in the heap, then you will never win the game: no matter 1, 2, or 3 stones you remove, the last stone will always be removed by your friend.  

## Idea:  
一开始的想法是如果我拿掉1块、2块、3块石头，Nim都会赢，那么是我输，否则是我赢。而这个可以通过递归实现。所以代码如下：  
```cpp
class Solution {
public:
    bool canWinNim(int n) {
        if(n==1||n==2||n==3) return 1;
        else
        {
            if(canWinNim(n-1)==1&&canWinNim(n-2)==1&&canWinNim(n-3)==1)//Nim Wins
            {
                return 0;
            }
            else return 1;
        }
    }
};
```
提交后出现了Time Limit Exceeded `//leetcode上递归有风险=。=`  
所以后来根据上面的想法，列出了前面几项的输出值：11101110...  
发现n为4的倍数时输出为0。  
所以最后代码：
```cpp
class Solution {
public:
    bool canWinNim(int n) {
        if(n%4==0)
        return false;
        else
        return true;
        }
};
```
PS:作为一个渣渣，第一题果断选了通过率最高的题目，但还是出现了一些小问题T T  
嗯木事木事坚持就好~
   
  
