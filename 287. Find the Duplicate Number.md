#Find the Duplicate Number
##Problem:
Given an array nums containing n + 1 integers where each integer is between 1 and n (inclusive), prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the duplicate one.

Note:
You must not modify the array (assume the array is read only).
You must use only constant, O(1) extra space.
Your runtime complexity should be less than O(n2).
There is only one duplicate number in the array, but it could be repeated more than once.
##Idea:
Method of exhaustion->O(n2) Time Limit Exceeded
##To Study:
`Two Pointers`-fast and slow
```cpp
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int slow=nums[0];
        int fast=nums[nums[0]];
        while(slow!=fast)
        {
            slow=nums[slow];
            fast=nums[nums[fast]];
        }
        fast=0;
        while(slow!=fast)
        {
            slow=nums[slow];
            fast=nums[fast];
        }
        return slow;
    }
};
//Time:O(n) Space:O(1)
```
**No need to worry about nums[i]=i, because that means there is an entry to i and both the entry number and i points to i, so i is the duplicate number.**  
`Binary Search`
>Let count be the number of elements in the range 1 .. mid.

>If count > mid, then there are more than mid elements in the range 1 .. mid and thus that range contains a duplicate.

>If count <= mid, then there are n+1-count elements in the range mid+1 .. n. That is, at least n+1-mid elements in a range of size n-mid. Thus this range must contain a duplicate.  

```cpp
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int n=(int)nums.size()-1;
        int low=1;
        int high=n;
        int mid=(low+high)/2;
        while(low<high)
        {
            int count=0;
            for(int i=0;i<nums.size();i++)
            {
                if(nums[i]>=low&&nums[i]<=mid) count++;
            }
            if(count>mid-low+1) high=mid;
            else low=mid+1;
            mid=(low+high)/2;
        }
        return low;
    }
};
//Time:O(nlogn) Space:O(1)
```
