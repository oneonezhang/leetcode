#Power of Two
##Problem:
Given an integer, write a function to determine if it is a power of two.
##Idea:
only have one '1' in binary format
```cpp
class Solution {
public:
    bool isPowerOfTwo(int n) {
        if(n<=0) return false;
        return ((n&(n-1))==0);
    }
};
```
**Pay Attention to the Operator Priority**