#Number of 1 Bits
##Problem:
Write a function that takes an unsigned integer and returns the number of ’1' bits it has (also known as the Hamming weight).

For example, the 32-bit integer ’11' has binary representation 00000000000000000000000000001011, so the function should return 3.
##Idea:
`bitmask`
```cpp
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int count=0;
        uint32_t mask=1;
        while(mask)
        {
            if(n&mask) count++;
            mask <<= 1;
        }
        return count;
    }
};
```
##To Study:
we can use n=n&(n-1) to clear the least significant 1
```cpp
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int count=0;
        while(n)
        {
            n=n&(n-1);
            count++;
        }
        return count;
    }
};
```