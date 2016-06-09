#Power of Four
##Problem:
Given an integer (signed 32 bits), write a function to check whether it is a power of 4.

Example:
Given num = 16, return true. Given num = 5, return false.

Follow up: Could you solve it without loops/recursion?
##Idea:
1. only has one bit of 1  
2. 1 appears at even bits:b0,b2,...,b30
```cpp
class Solution {
public:
    bool isPowerOfFour(int num) {
        return (num&(num-1))==0 && (num&0x55555555)!=0;
    }
};
```
##To Study:
we can also use (n-1)%3==0 to replace (num&0x55555555)!=0