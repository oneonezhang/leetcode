#Super Ugly Number
##Problem:
Write a program to find the nth super ugly number.

Super ugly numbers are positive numbers whose all prime factors are in the given prime list primes of size k. For example, [1, 2, 4, 7, 8, 13, 14, 16, 19, 26, 28, 32] is the sequence of the first 12 super ugly numbers given primes = [2, 7, 13, 19] of size 4.

Note:
(1) 1 is a super ugly number for any given primes.
(2) The given numbers in primes are in ascending order.
(3) 0 < k ≤ 100, 0 < n ≤ 106, 0 < primes[i] < 1000.
##Idea:
`Dynamic Programming` similar to Ugly Number II
```cpp
class Solution {
public:
    int nthSuperUglyNumber(int n, vector<int>& primes) {
        vector<int> uglyNums(n,INT_MAX);//INT_MAX is indispensable
        uglyNums[0]=1;
        vector<int> primesNo(primes.size());
        for(int i=1;i<n;i++)
        {
            for(int j=0;j<primes.size();j++)
            {
                uglyNums[i]=min(uglyNums[i],uglyNums[primesNo[j]]*primes[j]);
            }
            for(int j=0;j<primes.size();j++)
            {
                if(uglyNums[i]==uglyNums[primesNo[j]]*primes[j]) primesNo[j]++;
            }
        }
        return uglyNums[n-1];
    }
};
```
Time Complexity:O(nk)
##To Study:
`Heap`
```cpp
struct HeapNode
{
    int val;
    int index;
    int prime;
    HeapNode(int _val,int _index,int _prime):val(_val),index(_index),prime(_prime){}
    inline bool operator>(const HeapNode& another) const //Pay attention to const!
    {
        return val>another.val;
    }
};
class Solution {
public:
    int nthSuperUglyNumber(int n, vector<int>& primes) {
        vector<int> uglyNums(n);
        uglyNums[0]=1;
        priority_queue<HeapNode,vector<HeapNode>,greater<HeapNode>> minHeap;
        for(int p:primes) minHeap.push(HeapNode(p,0,p));
        for(int i=1;i<n;i++)
        {
            uglyNums[i]=minHeap.top().val;
            HeapNode nextNode=minHeap.top();
            while(nextNode.val==uglyNums[i])
            {
                minHeap.pop();
                nextNode.index++;
                nextNode.val=uglyNums[nextNode.index]*nextNode.prime;
                minHeap.push(nextNode);
                nextNode=minHeap.top();
            }
        }
        return uglyNums[n-1];
    }
};
```
