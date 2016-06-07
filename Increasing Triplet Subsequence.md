#Increasing Triplet Subsequence
##Problem:
Given an unsorted array return whether an increasing subsequence of length 3 exists or not in the array.

Formally the function should:  
Return true if there exists i, j, k   
such that arr[i] < arr[j] < arr[k] given 0 ≤ i < j < k ≤ n-1 else return false.  
Your algorithm should run in O(n) time complexity and O(1) space complexity.

Examples:  
Given [1, 2, 3, 4, 5],  
return true.

Given [5, 4, 3, 2, 1],  
return false.
##Idea:
Modify from `Longest Increasing Subsequence`
```cpp
class Solution {
public:
    bool increasingTriplet(vector<int>& nums) {
        if(nums.empty()) return false;
        vector<int> record(3);
        record[0]=nums[0];
        int currentPosition=0;
        for(int i=1;i<nums.size();i++)
        {
            if(nums[i]>nums[currentPosition])
            {
                currentPosition++;
                if(currentPosition==2) return true;
                nums[currentPosition]=nums[i];
            }
            else
            {
                for(int j=0;j<=currentPosition;j++)
                {
                    if(nums[j]>=nums[i])
                    {
                        nums[j]=nums[i];
                        break;
                    }
                }
            }
        }
        return false;
    }
};
```
##To Study:
A more clean way
```cpp
class Solution {
public:
    bool increasingTriplet(vector<int>& nums) {
        int length1=INT_MAX,length2=INT_MAX;
        for(int i=0;i<nums.size();i++)
        {
            if(nums[i]<=length1) length1=nums[i];
            else if(nums[i]<=length2) length2=nums[i];
            else return true;
        }
        return false;
    }
};
```