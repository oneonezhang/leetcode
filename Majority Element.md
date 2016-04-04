#Majority Element
##Problem:
Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always exist in the array.
##Idea:
`sort`
```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        return nums[(nums.size()-1)/2];
    }
};
```
##To Study:
1.`Sort`  
replace 'sort' with 'nth_element' to be faster.  
`nth_element(nums.begin(),nums.begin()+nums.size()/2,nums.end());`  
2.`Divide And Conquer`  
```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
    return majority(nums,0,nums.size());     
    }
private:
    int majority(vector<int>& nums,int begin,int end)
    {
        if(end-begin==1) return nums[begin];
        int leftMajority=majority(nums,begin,(begin+end)/2);
        int rightMajority=majority(nums,(begin+end)/2,end);
        if(leftMajority==rightMajority) return leftMajority;
        else
        {
            return (count(nums.begin()+begin,nums.begin()+end,leftMajority)>count(nums.begin()+begin,nums.begin()+end,rightMajority))?
                                                                                    leftMajority:rightMajority;
        }
    }
};
```
3.`Randomization`
```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int major;
        srand(time(0));
        while(true)
        {
            major=nums[random()%nums.size()];
            int count=0;
            for(int i=0;i<nums.size();i++)
            {
                if(nums[i]==major)
                    count++;
            }
            if(count>nums.size()/2) return major;
        }
    }
};
```
4.`Bit Manipulation`
```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int mask=1;
        int result=0;
        for(int i=0;i<32;i++)
        {
            int count=0;
            for(int j=0;j<nums.size();j++)
            {
                if(nums[j]&mask) count++;
            }
            if(count>nums.size()/2) result |= mask;
            mask=mask<<1;
        }
        return result;
    }
};
```
5.`Moore Voting Algorithm`  
```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int candidate;
        int count=0;
        for(int i=0;i<nums.size();i++)
        {
            if(count==0) 
            {
                count++;
                candidate=nums[i];
            }
            else if(nums[i]==candidate)
            {
                count++;
            }
            else
            {
                count--;
            }
        }
        return candidate;
    }
};
```
