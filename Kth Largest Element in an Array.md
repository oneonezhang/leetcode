#Kth Largest Element in an Array
##Problem:
Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

For example,
Given [3,2,1,5,6,4] and k = 2, return 5.

Note: 
You may assume k is always valid, 1 ≤ k ≤ array's length.
##Idea:
partition, partial sort
```cpp
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        int left=0;
        int right=nums.size()-1;
        int pos=partition(nums,left,right);
        while(pos!=k-1)
        {
            if(pos<k-1) left=pos+1;
            else right=pos-1;
            pos=partition(nums,left,right);
        }
        return nums[k-1];
    }
private:
    int partition(vector<int>& nums,int left,int right)
    {
        int nextLarger=left;
        for(int i=left;i<right;i++)
        {
            if(nums[i]>nums[right]) 
            {
                swap(nums[nextLarger],nums[i]);
                nextLarger++;
            }
        }
        swap(nums[nextLarger],nums[right]);
        return nextLarger;
    }
};
```
Time:best->O(n),worst->O(n2),average->O(n):T(n)=T(n/2)+O(n)
##To Study:
1. Heap
```cpp
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        priority_queue<int> maxheap(nums.begin(),nums.end());
        for(int i=0;i<k-1;i++)
            maxheap.pop();
        return maxheap.top();
    }
};
```
Time:O(n+klogn)  
Or we can build a k-size min-heap and time complexity is O(nlogk)  
2. random-quicksort  
random index
```cpp
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        int left=0;
        int right=nums.size()-1;
        int pos=partition(nums,left,right);
        while(pos!=k-1)
        {
            if(pos<k-1) left=pos+1;
            else right=pos-1;
            pos=partition(nums,left,right);
        }
        return nums[k-1];
    }
private:
    int partition(vector<int>& nums,int left,int right)
    {
        //choose a random pivot
        int randIndex=left+rand()%(right-left+1);
        swap(nums[randIndex],nums[right]);
        int nextLarger=left;
        for(int i=left;i<right;i++)
        {
            if(nums[i]>nums[right]) 
            {
                swap(nums[nextLarger],nums[i]);
                nextLarger++;
            }
        }
        swap(nums[nextLarger],nums[right]);
        return nextLarger;
    }
};
```
Or do shuffle at first
```cpp
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        //shuffle
        for(int i=1;i<nums.size();i++)
        {
            int swapIndex=rand()%(i+1);
            swap(nums[swapIndex],nums[i]);
        }
        int left=0;
        int right=nums.size()-1;
        int pos=partition(nums,left,right);
        while(pos!=k-1)
        {
            if(pos<k-1) left=pos+1;
            else right=pos-1;
            pos=partition(nums,left,right);
        }
        return nums[k-1];
    }
private:
    int partition(vector<int>& nums,int left,int right)
    {
        int nextLarger=left;
        for(int i=left;i<right;i++)
        {
            if(nums[i]>nums[right]) 
            {
                swap(nums[nextLarger],nums[i]);
                nextLarger++;
            }
        }
        swap(nums[nextLarger],nums[right]);
        return nextLarger;
    }
};
```
