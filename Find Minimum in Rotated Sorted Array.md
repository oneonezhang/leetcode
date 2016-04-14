#Find Minimum in Rotated Sorted Array
##Problem:
Suppose a sorted array is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

Find the minimum element.

You may assume no duplicate exists in the array.
##Idea:
1.check from begin to end
```cpp
class Solution {
public:
    int findMin(vector<int>& nums) {
        if(nums[0]<=nums.back()) return nums[0];
        for(int i=1;i<nums.size();i++)
        {
            if(nums[i]<nums[i-1]) return nums[i];
        }
    }
};
```
Time Complexity:O(n)  
2.`Binary Search`
```cpp
class Solution {
public:
    int findMin(vector<int>& nums) {
        int left=0;
        int right=(int)nums.size()-1;
        while(left<right)
        {
            if(nums[left]<nums[right]) return nums[left];
            int mid=(left+right)/2;
            if(nums[left]<=nums[mid]) left=mid+1;//Don't forget '=' in '<='
            else right=mid;
        }
        return nums[left];
    }
};
```
Time Complexity:O(logn)
