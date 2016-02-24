#Product of Array Except Self
##Problem:
Given an array of n integers where n > 1, nums, return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].

Solve it without division and in O(n).

For example, given [1,2,3,4], return [24,12,8,6].

Follow up:
Could you solve it with constant space complexity? (Note: The output array does not count as extra space for the purpose of space complexity analysis.)
##Idea:
本来想用分治法的，但是时间复杂度O(nlogn)。。。
##TO Study:
先从前往后累乘，再从后往前累乘，正好跳过自己。
```cpp
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
        int n = nums.size();
        vector<int> output(n);
        output[0] = 1;
        int endToBegin = 1;
        for(int i=1;i<nums.size();i++)
        {
            output[i] = output[i-1] * nums[i-1];
        }

        for(int i=n-2;i>=0;i--)
        {
            endToBegin *= nums[i+1];
            output[i] *= endToBegin;
        }
        return output;
    }
};
```