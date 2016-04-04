#Search Insert Position
##Problem:
Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

Here are few examples.  
[1,3,5,6], 5 → 2  
[1,3,5,6], 2 → 1  
[1,3,5,6], 7 → 4  
[1,3,5,6], 0 → 0  
##Idea:
```cpp
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int i=0;
        for(;i<nums.size();i++)
        {
            if(nums[i]>=target) break;;
        }
        return i;
    }
};
//Time:O(n)
```
##To Study:
`Binary Search`
```cpp
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int left=0;
        int right=(int)nums.size();
        int mid=(left+right)/2;
        while(left<right)
        {
            if(target==nums[mid]) return mid;
            else if(target<nums[mid]) right=mid;
            else left=mid+1;
            mid=(left+right)/2;
        }
        return mid;
    }
};
//Time:O(lgn)
```

