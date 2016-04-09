#Happy Number
##Problem:
Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

Example: 19 is a happy number

12 + 92 = 82  
82 + 22 = 68  
62 + 82 = 100  
12 + 02 + 02 = 1  
##Idea:
`Two Pointers`循环链
```cpp
class Solution {
public:
    bool isHappy(int n) {
        int slow=n;
        int fast=n;
        while(fast!=1)
        {
            slow=sumOfSquare(slow);
            fast=sumOfSquare(fast);
            fast=sumOfSquare(fast);
            if(slow==fast&&fast!=1) return false;
        }
        return true;
    }
private:
    int sumOfSquare(int n)
    {
        int sum=0;
        while(n)
        {
            sum += (n%10)*(n%10);
            n /= 10;
        }
        return sum;
    }
};
```
##To Study:
`Hash Table`
```cpp
class Solution {
public:
    bool isHappy(int n) {
        unordered_set<int> record;
        n=sumOfSquare(n);
        if(n==1) return true;
        while(record.find(n)==record.end())
        {
            record.insert(n);
            n=sumOfSquare(n);
            if(n==1) return true;
        }
        return false;
    }
private:
    int sumOfSquare(int n)
    {
        int sum=0;
        while(n)
        {
            sum += (n%10)*(n%10);
            n /= 10;
        }
        return sum;
    }
};
```