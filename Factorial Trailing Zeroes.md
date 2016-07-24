#Factorial Trailing Zeroes
##Problem:
Given an integer n, return the number of trailing zeroes in n!.

Note: Your solution should be in logarithmic time complexity.
##Idea:
factor 5 decides the number of trailing zeroes.
```cpp
class Solution {
public:
    int trailingZeroes(int n) {
        int count = 0;
        int base = 5;
        while(base<=n)
        {
            count += n/base;
            base *= 5;
        }
        return count;
    }
};
```
**Wrong Answer:1808548329, int overflow**
```cpp
class Solution {
public:
    int trailingZeroes(int n) {
        int count = 0;
        int base = 1;
        int boundary=n/5;
        while(base<=boundary)
        {
            base *= 5;
            count += n/base;
        }
        return count;
    }
};
```
##To Study:
```cpp
class Solution {
public:
    int trailingZeroes(int n) {
        int count = 0;
        while(n)
        {
            count += n/5;
            n /= 5;
        }
        return count;
    }
};
```