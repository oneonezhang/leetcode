#Counting Bits
##Problem:
Given a non negative integer number num. For every numbers i in the range 0 ≤ i ≤ num calculate the number of 1's in their binary representation and return them as an array.

Example:
For num = 5 you should return [0,1,1,2,1,2].

Follow up:

+ It is very easy to come up with a solution with run time O(n*sizeof(integer)). But can you do it in linear time O(n) /possibly in a single pass?
+ Space complexity should be O(n).
+ Can you do it like a boss? Do it without using any builtin function like __builtin_popcount in c++ or in any other language.  

#Idea:
每增加一位，前面的一串数加一
```cpp
class Solution {
public:
    vector<int> countBits(int num) {
        vector<int> result(num+1);
        int pointer=0;
        int end=1;
        result[0]=0;
        for(int i=1;i<=num;i++)
        {
            if(pointer==end)
            {
                pointer=0;
                end=i;
            }
            result[i]=result[pointer]+1;
            pointer++;
        }
        return result;
    }
};
```