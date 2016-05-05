#Sort Colors
##Problem:
Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

Note:  
You are not suppose to use the library's sort function for this problem.  
Follow up:  
A rather straight forward solution is a two-pass algorithm using counting sort.  
First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's.  

Could you come up with an one-pass algorithm using only constant space?
##Idea:
Use two variables whileLeft and whiteRight to record the possible boundary of white
```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int whiteLeft=0;
        int whiteRight=nums.size()-1;
        int current=0;
        while(current<=whiteRight)//break when the following objects are all blue
        {
            if(nums[current]==0)
            {
                swap(nums[whiteLeft],nums[current]);
                whiteLeft++;
                current++;
            }
            else if(nums[current]==2)
            {
                swap(nums[whiteRight],nums[current]);
                whiteRight--;
            }
            else current++;
        }
    }
};
```
##To Study:
1.`Two Pass Algorithm`——Count
```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int red=0;
        int white=0;
        int blue=0;
        int i;
        for(i=0;i<nums.size();i++)
        {
            if(nums[i]==0) red++;
            else if(nums[i]==1) white++;
            else blue++;
        }
        for(i=0;i<red;i++) nums[i]=0;
        for(;i<red+white;i++) nums[i]=1;
        for(;i<red+white+blue;i++) nums[i]=2;
    }
};
```
2.label the end of each color
```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
        int red=-1;
        int white=-1;
        int blue=-1;
        for(int i:nums)
        {
            if(i==0)
            {
                //All the colors should move one step to right
                nums[++blue]=2;
                nums[++white]=1;
                nums[++red]=0;
            }
            else if(i==1)
            {
                //Blue and white should move one step to right
                nums[++blue]=2;
                nums[++white]=1;
            }
            else
            nums[++blue]=2;//Only blue should move one step to right
        }
    }
};
```
