# Single Number  
## Problem:  
Given an array of integers, every element appears twice except for one. Find that single one.

Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?  
##Idea:  
因为对Hash Table和Bit Manipulation并不是很了解，所以用了一种很愚蠢的办法。定义了一个长度为65536的bool型数组，下标为题目中整数数组元素可能的值，来记录每个值出现次数的奇偶性。  
第一次提交的时候没有考虑到负数的情况，所以出现了Runtime Error，所以后来又加上了对负数的判定及处理。
```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        bool count[65536]={0};
        for(int i=0;i<nums.size();i++)
        {
            if(nums[i]<0)
                nums[i]+=65536;
            count[nums[i]]=!count[nums[i]];
        }
        for(int i=0;i<65536;i++)
        {
            if(count[i])
            {
                if(i>=32768)
                i-=65536;
                return i;
            }
        }
    }
};
```  
## TO STUDY:
1.Bit Manipulation  
看了讨论区，才知道c++也是有按位运算也是有异或的。  
主要性质：`0^a=a   a^a=0  a^a^b=b`  
所以代码如下：
```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int result=0;
        for(int i=0;i<nums.size();i++)
        {
            result=result^nums[i];
        }
        return result;
    }
};
```
2.Hash Table  
因为对STL和iterator不是很了解，姑且学着写了一个。//话说时间好像比上面的慢了1倍=。=  
```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        unordered_map<int,int> count=unordered_map<int,int>();
        for(int i=0;i<nums.size();i++)
        {
            if(count.find(nums[i])!=count.end())
            {
                count.erase(nums[i]);
            }
            else
            {
                count.insert(unordered_map<int,int>::value_type(nums[i],1));//count[nums[i]]=1;
            }
        }
        if(count.begin()!=count.end()) return count.begin()->first;//begin()==end() the container is empty
        else return 0;
    }
};
```
