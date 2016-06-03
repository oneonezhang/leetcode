#Remove Element
##Problem:
Given an array and a value, remove all instances of that value in place and return the new length.

Do not allocate extra space for another array, you must do this in place with constant memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

Example:
Given input array nums = [3,2,2,3], val = 3

Your function should return length = 2, with the first two elements of nums being 2.
##Idea:
`Two Pointers`  
1.The order is not changed
```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int nextNot=0;
        for(int scanner=0;scanner<nums.size();scanner++)
        {
            if(nums[scanner]!=val)
            {
                nums[nextNot]=nums[scanner];
                nextNot++;
            }
        }
        return nextNot;
    }
};
```
2.The order is changed  
Work well when the elements to remove are rare
```cpp
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int right=nums.size()-1;
        for(int scanner=nums.size()-1;scanner>=0;scanner--)
        {
            if(nums[scanner]==val)
            {
                nums[scanner]=nums[right];
                right--;
            }
        }
        return right+1;
    }
};
```