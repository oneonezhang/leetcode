#Missing Number
##Problem:
Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.

For example,
Given nums = [0, 1, 3] return 2.

Note:
Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?
##Idea:
`SUM`
```cpp
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int  n=nums.size();
        int sum=0;
        for(int i=0;i<n;i++)
        {
            sum += nums[i];
        }
        return (n+1)*n/2-sum;
    }
};
```
##To Study:
`Sum may be overflow`  
`Bit Manipulation`
```cpp
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int result=nums.size();
        for(int i=0;i<nums.size();i++)
        {
            result ^= nums[i]^i;
        }
        return result;
    }
};
```