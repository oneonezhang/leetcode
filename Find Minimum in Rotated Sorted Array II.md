#Find Minimum in Rotated Sorted Array II
##Problem:
>Follow up for "Find Minimum in Rotated Sorted Array":  
>What if duplicates are allowed?
>  
>Would this affect the run-time complexity? How and why?

Suppose a sorted array is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

Find the minimum element.

The array may contain duplicates.
##Idea:
`Binary Search`  
case:nums[left]==nums[mid] is different from the original problem,  
since it can be either nums[mid]=nums[mid+1]=...=nums[left] or nums[left]=nums[left+1]=...=nums[mid].  
We need to check whether the minimum is in the left part or not.  
Therefore, time complexity will grow when nums[left]==nums[mid]&&minimum is not in the left part.  
But anyway, it's between O(logn) and 0(n).
```cpp
class Solution {
public:
    int findMin(vector<int>& nums) {
        return helper(nums,0,nums.size()-1);
    }
private:
    int helper(vector<int>& nums,int left,int right)
    {
        if(left==right) return nums[left];
        else if(nums[left]<nums[right]) return nums[left];
        int mid=(left+right)/2;
        if(nums[left]<nums[right]) return helper(nums,mid+1,right);
        else if(nums[left]>nums[mid]) return helper(nums,left,mid);
        else
        {
            int temp=helper(nums,left,mid);
            if(nums[left]>temp) return temp;
            else return helper(nums,mid+1,right);
        }
    }
};
```
##To Study:
1.when nums[left]==nums[mid]  
we can think that left isn't minimum and simply left++  
2.binary search bug  
when left+right is too large, it may overflow and become negative  
so `int mid = left+(right-left)/2` is better