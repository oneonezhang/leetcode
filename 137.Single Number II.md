#Single Number II  
##Problem:  
Given an array of integers, every element appears three times except for one. Find that single one.

Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?  
##Idea:  
`hash table`
```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        unordered_map<int,int> hash=unordered_map<int,int>();
        for(int i=0;i<nums.size();i++)
        {
            if(hash.find(nums[i])!=hash.end())
            {
                hash[nums[i]]=hash[nums[i]]+1;
                if(hash[nums[i]]==3)
                {
                    hash.erase(nums[i]);               
                }

            }
            else
            {
                hash[nums[i]]=1;
            }
        }
        return hash.begin()->first;
    }
};
```  
##To Study:  
1.`count`  
```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
    int count[32]={0};
    int result=0;
    for(int i=0;i<32;i++)
    {
        for(int j=0;j<nums.size();j++)
        {
            if(nums[j]>>i&1)
                count[i]++;
        }
        result |= (count[i]%3)<<i;
    }
    return result;
    }
};
```  
2.`bit mask` //faster
(1)
```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int ones=0,twos=0;
        for(int i=0;i<nums.size();i++)
        {
            twos |= ones&nums[i];
            ones ^= nums[i];
            int notthree=~(twos&ones);
            twos &= notthree;
            ones &= notthree;
        }
        return ones;
    }
};
```
(2)
```cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
    int x0=0xffffffff,x1=0,x2=0,t;//x0=~0
    for(int i=0;i<nums.size();i++)
    {
        t=x2;
        x2=(x1&nums[i])|(x2&~nums[i]);
        x1=(x0&nums[i])|(x1&~nums[i]);
        x0=(t&nums[i])|(x0&~nums[i]);
    }
    return x1;
    }
};
```  
(3)Given an array of integers, every element appears k times except for one. Find that single one who appears l times.  
```cpp
public class Solution {
    int singleNumber(int A[], int k, int l) {
        int t;
        int x[k]={0};
        x[0] = ~0;
        for (int i = 0; i < A.size(); i++) {
            t = x[k-1];
            for (int j = k-1; j > 0; j--) {
                x[j] = (x[j-1] & A[i]) | (x[j] & ~A[i]);
            }
            x[0] = (t & A[i]) | (x[0] & ~A[i]);
        }
        return x[l];
    }
}
```
 
