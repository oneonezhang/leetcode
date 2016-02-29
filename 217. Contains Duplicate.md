#Contains Duplicate
##Problem:
Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.
##Idea:
Hash Table
```cpp
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        unordered_map<int,int> count;
        for(int i=0;i<nums.size();i++)
        {
            if(count.find(nums[i])!=count.end())
            {
                count[nums[i]]++;
            }
            else
            {
                count[nums[i]]=1;
            }
        }
        for(auto each:count)
        {
            if(each.second>1) return 1;
        }
        return 0;
    }
};
```
##To Study:
1.`sort`  
  `注意：size()返回值为无符号整数`
```cpp
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        int n=nums.size();
        for(int i=0;i<n-1;i++)
        {
            if(nums[i]==nums[i+1]) return 1;
        }
        return 0;
    }
};
```
```cpp
//Unique and Erase
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        int n=nums.size();
        nums.erase(unique(nums.begin(),nums.end()),nums.end());
        return(n!=nums.size());
    }
};
```
2.`set`  
`1 LOC`
```cpp
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        return (set<int>(nums.begin(),nums.end()).size() != nums.size());
    }
};
```