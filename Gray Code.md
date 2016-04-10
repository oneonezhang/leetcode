#Gray Code
##Problem:
The gray code is a binary numeral system where two successive values differ in only one bit.

Given a non-negative integer n representing the total number of bits in the code, print the sequence of gray code. A gray code sequence must begin with 0.

For example, given n = 2, return [0,1,3,2]. Its gray code sequence is:

00 - 0  
01 - 1  
11 - 3  
10 - 2  
##Idea:
`recursion`
```cpp
class Solution {
public:
    vector<int> grayCode(int n) {
        vector<int> gray(pow(2,n));
        if(n==0)
        {
            gray[0]=0;
        }
        else
        {
            vector<int> grayBefore=grayCode(n-1);
            for(int i=0;i<grayBefore.size();i++)
            {
                gray[i]=grayBefore[i];
                gray[2*grayBefore.size()-1-i]=grayBefore[i]+(1<<n-1);
            }
        }
        return gray;
    }
};
```
##To Study:
1.`according to definition`
```cpp
class Solution {
public:
    vector<int> grayCode(int n) {
        vector<int> gray(1<<n);
        for(int i=0;i<(1<<n);i++)
        {
            gray[i]=i^(i>>1);
        }
        return gray;
    }
};
```
2.`iteration`
```cpp
class Solution {
public:
    vector<int> grayCode(int n) {
        vector<int> gray={0};
        for(int bit=0;bit<n;bit++)
        {
            for(int pointer=gray.size()-1;pointer>=0;pointer--)
            {
                gray.push_back((1<<bit)+gray[pointer]);
            }
        }
        return gray;
    }
};
```