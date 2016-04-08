#Maximum Subarray
##Problem:
Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array [−2,1,−3,4,−1,2,1,−5,4],  
the contiguous subarray [4,−1,2,1] has the largest sum = 6.
##Idea:
1.`Kadane's Algorithm`
```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int maxEndingHere=nums[0];
        int maxSum=nums[0];
        for(int i=1;i<nums.size();i++)
        {
            maxEndingHere=max(nums[i],maxEndingHere+nums[i]);
            maxSum=max(maxSum,maxEndingHere);
        }
        return maxSum;
    }
};
```
2.`Divide and Conquer`
```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        if(nums.empty()) return 0;
        else return helper(nums,0,nums.size());
    }
private:
    int helper(vector<int>& nums,int left,int right)
    {
        if(right-left>1)
        {
            int mid=(left+right)/2;
            int leftMax=helper(nums,left,mid);
            int rightMax=helper(nums,mid,right);
            int toLeft=nums[mid-1];
            int leftPart=nums[mid-1];
            int toRight=nums[mid];
            int rightPart=nums[mid];
            for(int i=mid-2;i>=left;i--)
            {
                toLeft += nums[i];
                if(toLeft>leftPart) leftPart=toLeft;
            }
            for(int i=mid+1;i<right;i++)
            {
                toRight += nums[i];
                if(toRight>rightPart) rightPart=toRight;
            }
            int maxSum=max(leftMax,rightMax);
            maxSum=max(maxSum,leftPart+rightPart);
            return maxSum;
        }
        else
        {
            return nums[left];
        }
    }
};
```