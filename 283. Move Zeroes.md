#Move Zeroes
##Problem:
Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

For example, given nums = [0, 1, 0, 3, 12], after calling your function, nums should be [1, 3, 12, 0, 0].

Note:
You must do this in-place without making a copy of the array.
Minimize the total number of operations.
##Idea:
与快排中的partition部分同理
```cpp
class Solution {
public:
    void moveZeroes(vector<int>& nums) {
        int nextToSwap=0;
        for(int nextToRead=0;nextToRead<nums.size();nextToRead++)
        {
            if(nums[nextToRead])
            {
                int temp=nums[nextToRead];
                nums[nextToRead]=nums[nextToSwap];
                nums[nextToSwap]=temp;
                nextToSwap++;
            }
        }
    }
};
```