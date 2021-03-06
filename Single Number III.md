#Single Number III
##Problem:  
Given an array of numbers nums, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once.

For example:

Given nums = [1, 2, 1, 3, 2, 5], return [3, 5].

Note:
The order of the result is not important. So in the above example, [5, 3] is also correct.
Your algorithm should run in linear runtime complexity. Could you implement it using only constant space complexity?
##Idea:
继续用哈希表
##To Study:
`classification`
```cpp
class Solution {
public:
    vector<int> singleNumber(vector<int>& nums) {
        int xorOfTwo=0;
        for(int i=0;i<nums.size();i++)
        {
            xorOfTwo ^= nums[i];
        }
        int oneBit=xorOfTwo & -xorOfTwo;//find the first bit which is 1 from right to left 
                                        //Two's Complement Form
        vector<int> result={0,0};
        for(int i=0;i<nums.size();i++)
        {
            if(nums[i]&oneBit)
                result[0] ^= nums[i];
        }
        result[1]=result[0]^xorOfTwo;
        return result;
    }
};
```
