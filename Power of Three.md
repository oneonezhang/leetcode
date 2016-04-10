#Power of Three
##Problem:
Given an integer, write a function to determine if it is a power of three.

Follow up:
Could you do it without using any loop / recursion?
##Idea:
loop / recursion
##To Study:
1.find the maximum power of 3
```cpp
class Solution {
public:
    bool isPowerOfThree(int n) {
        if(n<=0) return false;
        int maxPowerOf3=pow(3,(int)(log(0x7fffffff)/log(3)));
        return (maxPowerOf3%n==0);
    }
};
```
2.log3(n) is an integer?
```cpp
class Solution {
public:
    bool isPowerOfThree(int n) {
        return fmod(log10(n)/log10(3),1)==0;//log(243)/log(3) error
    }
};
```
3.another way to judge if log3(n) is an integer
```cpp
class Solution {
public:
    bool isPowerOfThree(int n) {
        if(n<=0) return false;
        int counter=round(log(n)/log(3));
        return n==pow(3,counter);
    }
};
```

