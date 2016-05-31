#Longest Increasing Subsequence
##Problem:
Given an unsorted array of integers, find the length of longest increasing subsequence.

For example,  
Given [10, 9, 2, 5, 3, 7, 101, 18],  
The longest increasing subsequence is [2, 3, 7, 101], therefore the length is 4. Note that there may be more than one LIS combination, it is only necessary for you to return the length.

Your algorithm should run in O(n2) complexity.

Follow up: Could you improve it to O(n log n) time complexity?
##Idea:
use maxLen[i] to record the max length of subsequences which end with nums[i]——`Dynamic Programming`  
Time Complexity:O(n2)
```cpp
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        int result=0;
        vector<int> maxLen(nums.size());
        for(int i=0;i<maxLen.size();i++)
        {
            maxLen[i]=1;
            for(int j=0;j<i;j++)
            {
                if(nums[j]<nums[i])
                {
                    maxLen[i]=max(maxLen[i],maxLen[j]+1);
                }
            }
            result=max(result,maxLen[i]);
        }
        return result;
    }
};
```
##To Study:
`Binary Search`, `Variant of Patience Sorting`
helpArray[i] records the last number of subsequence whose length is i+1
```cpp
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        if(nums.empty()) return 0;
        vector<int> helpArray={nums[0]};
        for(int i=1;i<nums.size();i++)
        {
            if(nums[i]>helpArray.back()) helpArray.push_back(nums[i]);
            else
            {
                int left=0,right=helpArray.size()-1;
                int mid=left+(right-left)/2;
                while(left<right)
                {
                    if(helpArray[mid]<nums[i]) left=mid+1;
                    else right=mid;
                    mid=left+(right-left)/2;
                }
                helpArray[mid]=nums[i];
            }
        }
        return helpArray.size();
    }
};
```
we can also use `lower_bound` to do binary search
```cpp
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        if(nums.empty()) return 0;
        vector<int> helpArray={nums[0]};
        for(int i=1;i<nums.size();i++)
        {
            auto iterator=lower_bound(helpArray.begin(),helpArray.end(),nums[i]);
            if(iterator==helpArray.end()) helpArray.push_back(nums[i]);
            else
            *iterator=nums[i];
        }
        return helpArray.size();
    }
};
```